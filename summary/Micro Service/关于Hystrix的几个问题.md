# 关于Hystrix的几个问题

### 文章目录

- [概述](https://blog.csdn.net/qq_31960623/article/details/118882355#_5)
- [Hystrix之熔断和降级](https://blog.csdn.net/qq_31960623/article/details/118882355#Hystrix_11)
- [Hystrix解决了什么问题](https://blog.csdn.net/qq_31960623/article/details/118882355#Hystrix_56)
- [整体机制](https://blog.csdn.net/qq_31960623/article/details/118882355#_71)
- [熔断](https://blog.csdn.net/qq_31960623/article/details/118882355#_86)
- [资源隔离](https://blog.csdn.net/qq_31960623/article/details/118882355#_208)
- - [信号量模式](https://blog.csdn.net/qq_31960623/article/details/118882355#_214)
  - [线程池模式](https://blog.csdn.net/qq_31960623/article/details/118882355#_299)
- [超时检测](https://blog.csdn.net/qq_31960623/article/details/118882355#_391)
- [降级](https://blog.csdn.net/qq_31960623/article/details/118882355#_527)
- [健康统计](https://blog.csdn.net/qq_31960623/article/details/118882355#_645)
- [本文小结](https://blog.csdn.net/qq_31960623/article/details/118882355#_749)



## 概述

> Hystrix是Netflix（奈飞） 公司开源的一个项目，它提供了熔断器功能，能够阻止分布式系统中出现联动故障。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/1341411339149f1341e9dddc9b8832f3.png)

## Hystrix之熔断和降级

> 在分布式环境中，不可避免地会有许多服务依赖项中的某些失败。Hystrix是一个库，可通过添加等待时间容限和容错逻辑来帮助您控制这些分布式服务之间的交互。Hystrix通过隔离服务之间的访问点，停止服务之间的级联故障并提供后备选项来实现此目的，所有这些都可以提高系统的整体弹性。

总体来说 Hystrix 就是一个能进行 熔断 和 降级 的库，通过使用它能提高整个系统的弹性。那么什么是 熔断和降级 呢？再举个例子，此时我们整个微服务系统是这样的。服务A调用了服务B，服务B再调用了服务C，但是因为某些原因，服务C顶不住了，这个时候大量请求会在服务C阻塞。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/1db8b07a04a534b9d212f811575f7ce1.png)

服务C阻塞了还好，毕竟只是一个系统崩溃了。但是请注意这个时候因为服务C不能返回响应，那么服务B调用服务C的的请求就会阻塞，同理服务B阻塞了，那么服务A也会阻塞崩溃。

> 请注意，为什么阻塞会崩溃。因为这些请求会消耗占用系统的线程、IO 等资源，消耗完你这个系统服务器不就崩了么。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/bafe93803cc7d19a2f9673d63af1b876.png)

> 这就叫 服务雪崩。妈耶，上面两个 熔断 和 降级 你都没给我解释清楚，你现在又给我扯什么 服务雪崩 ？

所谓 熔断 就是服务雪崩的一种有效解决方案。当指定时间窗内的请求失败率达到设定阈值时，系统将通过 断路器 直接将此请求链路断开。

也就是我们上面服务B调用服务C在指定时间窗内，调用的失败率到达了一定的值，那么 Hystrix 则会自动将 服务B与C 之间的请求都断了，以免导致服务雪崩现象。

其实这里所讲的 熔断 就是指的 Hystrix 中的 断路器模式 ，你可以使用简单的 @HystrixCommand 注解来标注某个方法，这样 Hystrix 就会使用 断路器 来“包装”这个方法，每当调用时间超过指定时间时(默认为1000ms)，断路器将会中断对这个方法的调用。

当然你可以对这个注解的很多属性进行设置，比如设置超时时间，像这样。

````java
@HystrixCommand(commandProperties = {@HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds",value = "1200")})
public List<Xxx> getXxxx() {
    // ...省略代码逻辑
}
````

但是，我查阅了一些博客，发现他们都将 熔断 和 降级 的概念混淆了，以我的理解，降级是为了更好的用户体验，当一个方法调用异常时，通过执行另一种代码逻辑来给用户友好的回复。这也就对应着 Hystrix 的 后备处理 模式。你可以通过设置 fallbackMethod 来给一个方法设置备用的代码逻辑。比如这个时候有一个热点新闻出现了，我们会推荐给用户查看详情，然后用户会通过id去查询新闻的详情，但是因为这条新闻太火了，大量用户同时访问可能会导致系统崩溃，那么我们就进行 服务降级 ，一些请求会做一些降级处理比如当前人数太多请稍后查看等等。

````java
// 指定了后备方法调用
@HystrixCommand(fallbackMethod = "getHystrixNews")
@GetMapping("/get/news")
public News getNews(@PathVariable("id") int id) {
    // 调用新闻系统的获取新闻api 代码逻辑省略
}
// 
public News getHystrixNews(@PathVariable("id") int id) {
    // 做服务降级
    // 返回当前人数太多，请稍后查看
}
````

## Hystrix解决了什么问题

在复杂的分布式应用中有着许多的依赖，各个依赖都难免会在某个时刻失败，如果应用不隔离各个依赖，降低外部的风险，那容易拖垮整个应用。

举个电商场景中常见的例子，比如订单服务调用了库存服务、商品服务、积分服务、支付服务，系统均正常情况下，订单模块正常运行。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/f216f1ccde252ad6557deedf2b78d280.png)

但是当积分服务发生异常时且会阻塞30s时，订单服务就会有部分请求失败，且工作线程阻塞在调用积分服务上。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/d452e3a98c6895b4d9b4b29533f2f914.png)

流量高峰时，问题会更加严重，订单服务的所有请求都会阻塞在调用积分服务上，工作线程全部挂起，导致机器资源耗尽，订单服务也不可用，造成级联影响，整个集群宕机，这种称为雪崩效应。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/cc43b7cc36826ccd00f258a2a87eb1a7.png)


所以需要一种机制，使得单个服务出现故障时，整个集群可用性不受到影响。Hystrix就是实现这种机制的框架，下面我们分析一下Hystrix整体的工作机制。

## 整体机制

【入口】Hystrix的执行入口是HystrixCommand或HystrixObservableCommand对象，通常在Spring应用中会通过注解和AOP来实现对象的构造，以降低对业务代码的侵入性；

【缓存】HystrixCommand对象实际开始执行后，首先是否开启缓存，若开启缓存且命中，则直接返回；

【熔断】若熔断器打开，则执行短路，直接走降级逻辑；若熔断器关闭，继续下一步，进入隔离逻辑。熔断器的状态主要基于窗口期内执行失败率，若失败率过高，则熔断器自动打开；

【隔离】用户可配置走线程池隔离或信号量隔离，判断线程池任务已满（或信号量），则进入降级逻辑；否则继续下一步，实际由线程池任务线程执行业务调用；

【执行】实际开始执行业务调用，若执行失败或异常，则进入降级逻辑；若执行成功，则正常返回；

【超时】通过定时器延时任务检测业务调用执行是否超时，若超时则取消业务执行的线程，进入降级逻辑；若未超时，则正常返回。线程池、信号量两种策略均隔离方式支持超时配置（信号量策略存在缺陷）；

【降级】进入降级逻辑后，当业务实现了HystrixCommand.getFallback() 方法，则返回降级处理的数据；当未实现时，则返回异常；

【统计】业务调用执行结果成功、失败、超时等均会进入统计模块，通过健康统计结果来决定熔断器打开或关闭。
都说源码里没有秘密，下面我们来分析下核心功能源码，看看Hystrix如何实现整体的工作机制。

## 熔断

家用电路中都有保险丝，保险丝的作用场景是，当电路发生故障或异常时，伴随着电流不断升高，并且升高的电流有可能损坏电路中的某些重要器件或贵重器件，也有可能烧毁电路甚至造成火灾。

若电路中正确地安置了保险丝，那么保险丝就会在电流异常升高到一定程度的时候，自身熔断切断电流，从而起到保护电路安全运行的作用。Hystrix提供的熔断器就有类似功能，应用调用某个服务提供者，当一定时间内请求总数超过配置的阈值，且窗口期内错误率过高，那Hystrix就会对调用请求熔断，后续的请求直接短路，直接进入降级逻辑，执行本地的降级策略。

Hystrix具有自我调节的能力，熔断器打开在一定时间后，会尝试通过一个请求，并根据执行结果调整熔断器状态，让熔断器在closed,open,half-open三种状态之间自动切换。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/cf8994121d197a6a3bdf19f0a35bd59a.png)

> 【HystrixCircuitBreaker】

boolean attemptExecution()：

每次HystrixCommand执行，都要调用这个方法，判断是否可以继续执行，若熔断器状态为打开且超过休眠窗口，更新熔断器状态为half-open；通过CAS原子变更熔断器状态来保证只放过一条业务请求实际调用提供方，并根据执行结果调整状态。

````java
public boolean attemptExecution() {
    //判断配置是否强制打开熔断器
    if (properties.circuitBreakerForceOpen().get()) {
        return false;
    }
    //判断配置是否强制关闭熔断器
    if (properties.circuitBreakerForceClosed().get()) {
        return true;
    }
    //判断熔断器开关是否关闭
    if (circuitOpened.get() == -1) {
        return true;
    } else {
        //判断请求是否在休眠窗口后
        if (isAfterSleepWindow()) {
            //更新开关为半开，并允许本次请求通过
            if (status.compareAndSet(Status.OPEN, Status.HALF_OPEN)) {
                return true;
            } else {
                return false;
            }
        } else {
            //拒绝请求
            return false;
        }
    }
}
````

> 【HystrixCircuitBreaker】

void markSuccess()：

HystrixCommand执行成功后调用，当熔断器状态为half-open，更新熔断器状态为closed。此种情况为熔断器原本为open，放过单条请求实际调用服务提供者，并且后续执行成功，Hystrix自动调节熔断器为closed。

````java
public void markSuccess() {
    //更新熔断器开关为关闭
    if (status.compareAndSet(Status.HALF_OPEN, Status.CLOSED)) {
        //重置订阅健康统计
        metrics.resetStream();
        Subscription previousSubscription = activeSubscription.get();
        if (previousSubscription != null) {
            previousSubscription.unsubscribe();
        }
        Subscription newSubscription = subscribeToStream();
        activeSubscription.set(newSubscription);
        //更新熔断器开关为关闭
        circuitOpened.set(-1L);
    }
}
````

> 【HystrixCircuitBreaker】

void markNonSuccess()：

HystrixCommand执行成功后调用，若熔断器状态为half-open，更新熔断器状态为open。此种情况为熔断器原本为open，放过单条请求实际调用服务提供者，并且后续执行失败，Hystrix继续保持熔断器打开，并把此次请求作为休眠窗口期开始时间。

````java
public void markNonSuccess() {
      //更新熔断器开关，从半开变为打开
      if (status.compareAndSet(Status.HALF_OPEN, Status.OPEN)) {
          //记录失败时间，作为休眠窗口开始时间
          circuitOpened.set(System.currentTimeMillis());
      }
  }
````



> 【HystrixCircuitBreaker】

void subscribeToStream()：

熔断器订阅健康统计结果，若当前请求数据大于一定值且错误率大于阈值，自动更新熔断器状态为opened，后续请求短路，不再实际调用服务提供者，直接进入降级逻辑。

````java
private Subscription subscribeToStream() {
    //订阅监控统计信息
    return metrics.getHealthCountsStream()
            .observe()
            .subscribe(new Subscriber<HealthCounts>() {
                @Override
                public void onCompleted() {}
                @Override
                public void onError(Throwable e) {}
                @Override
                public void onNext(HealthCounts hc) {
                    // 判断总请求数量是否超过配置阈值，若未超过，则不改变熔断器状态
                    if (hc.getTotalRequests() < properties.circuitBreakerRequestVolumeThreshold().get()) {

                    } else {
                        //判断请求错误率是否超过配置错误率阈值，若未超过，则不改变熔断器状态；若超过，则错误率过高，更新熔断器状态未打开，拒绝后续请求
                        if (hc.getErrorPercentage() < properties.circuitBreakerErrorThresholdPercentage().get()) {
     
                        } else {
                            if (status.compareAndSet(Status.CLOSED, Status.OPEN)) {
                                circuitOpened.set(System.currentTimeMillis());
                            }
                        }
                    }
                }
            });

}
````



## 资源隔离

在货船中，为了防止漏水和火灾的扩散，一般会将货仓进行分割，避免了一个货仓出事导致整艘船沉没的悲剧。同样的，在Hystrix中，也采用了这样的舱壁模式，将系统中的服务提供者隔离起来，一个服务提供者延迟升高或者失败，并不会导致整个系统的失败，同时也能够控制调用这些服务的并发度。如下图，订单服务调用下游积分、库存等服务使用不同的线程池，当积分服务故障时，只会把对应线程池打满，而不会影响到其他服务的调用。Hystrix隔离模式支持线程池和信号量两种方式。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/cda5d1b2604f703f0274256ae0ac936f.png)

## 信号量模式

信号量模式控制单个服务提供者执行并发度，比如单个CommondKey下正在请求数为N，若N小于maxConcurrentRequests，则继续执行；若大于等于maxConcurrentRequests，则直接拒绝，进入降级逻辑。信号量模式使用请求线程本身执行，没有线程上下文切换，开销较小，但超时机制失效。

> 【AbstractCommand】

ObservableapplyHystrixSemantics(finalAbstractCommand _cmd)：尝试获取信号量，若能获取到，则继续调用服务提供者；若不能获取到，则进入降级策略。

````java
private Observable<R> applyHystrixSemantics(final AbstractCommand<R> _cmd) {
    executionHook.onStart(_cmd);
    //判断熔断器是否通过
    if (circuitBreaker.attemptExecution()) {
        //获取信号量
        final TryableSemaphore executionSemaphore = getExecutionSemaphore();
        final AtomicBoolean semaphoreHasBeenReleased = new AtomicBoolean(false);
        final Action0 singleSemaphoreRelease = new Action0() {
            @Override
            public void call() {
                if (semaphoreHasBeenReleased.compareAndSet(false, true)) {
                    executionSemaphore.release();
                }
            }
        };
        final Action1<Throwable> markExceptionThrown = new Action1<Throwable>() {
            @Override
            public void call(Throwable t) {
                eventNotifier.markEvent(HystrixEventType.EXCEPTION_THROWN, commandKey);
            }
        };
        //尝试获取信号量
        if (executionSemaphore.tryAcquire()) {
            try {
                //记录业务执行开始时间
                executionResult = executionResult.setInvocationStartTime(System.currentTimeMillis());
                //继续执行业务
                return executeCommandAndObserve(_cmd)
                        .doOnError(markExceptionThrown)
                        .doOnTerminate(singleSemaphoreRelease)
                        .doOnUnsubscribe(singleSemaphoreRelease);
            } catch (RuntimeException e) {
                return Observable.error(e);
            }
        } else {
            //信号量拒绝，进入降级逻辑
            return handleSemaphoreRejectionViaFallback();
        }
    } else {
        //熔断器拒绝，直接短路，进入降级逻辑
        return handleShortCircuitViaFallback();
    }
}
````



> 【AbstractCommand】

TryableSemaphore getExecutionSemaphore()：

获取信号量实例，若当前隔离模式为信号量，则根据commandKey获取信号量，不存在时初始化并缓存；若当前隔离模式为线程池，则使用默认信号量TryableSemaphoreNoOp.DEFAULT，全部请求可通过。

````java
protected TryableSemaphore getExecutionSemaphore() {
    //判断隔离模式是否为信号量
    if (properties.executionIsolationStrategy().get() == ExecutionIsolationStrategy.SEMAPHORE) {
        if (executionSemaphoreOverride == null) {
            //获取信号量
            TryableSemaphore _s = executionSemaphorePerCircuit.get(commandKey.name());
            if (_s == null) {
                //初始化信号量并缓存
                executionSemaphorePerCircuit.putIfAbsent(commandKey.name(), new TryableSemaphoreActual(properties.executionIsolationSemaphoreMaxConcurrentRequests()));
                //返回信号量
                return executionSemaphorePerCircuit.get(commandKey.name());
            } else {
                return _s;
            }
        } else {
            return executionSemaphoreOverride;
        }
    } else {
        //返回默认信号量，任何请求均可通过
        return TryableSemaphoreNoOp.DEFAULT;
    }
}
````


## 线程池模式

线程池模式控制单个服务提供者执行并发度，代码上都会先走获取信号量，只是使用默认信号量，全部请求可通过，然后实际调用线程池逻辑。线程池模式下，比如单个CommondKey下正在请求数为N，若N小于maximumPoolSize，会先从 Hystrix 管理的线程池里面获得一个线程，然后将参数传递给任务线程去执行真正调用，如果并发请求数多于线程池线程个数，就有任务需要进入队列排队，但排队队列也有上限，如果排队队列也满，则进去降级逻辑。线程池模式可以支持异步调用，支持超时调用，存在线程切换，开销大。

> 【AbstractCommand】

ObservableexecuteCommandWithSpecifiedIsolation(final AbstractCommand _cmd)：从线程池中获取线程，并执行，过程中记录线程状态。

````java
private Observable<R> executeCommandWithSpecifiedIsolation(final AbstractCommand<R> _cmd) {
      //判断是否为线程池隔离模式
      if (properties.executionIsolationStrategy().get() == ExecutionIsolationStrategy.THREAD) {
          return Observable.defer(new Func0<Observable<R>>() {
              @Override
              public Observable<R> call() {
                  executionResult = executionResult.setExecutionOccurred();
                  if (!commandState.compareAndSet(CommandState.OBSERVABLE_CHAIN_CREATED, CommandState.USER_CODE_EXECUTED)) {
                      return Observable.error(new IllegalStateException("execution attempted while in state : " + commandState.get().name()));
                  }
                  //统计信息
                  metrics.markCommandStart(commandKey, threadPoolKey, ExecutionIsolationStrategy.THREAD);
                  //判断是否超时，若超时，直接抛出异常
                  if (isCommandTimedOut.get() == TimedOutStatus.TIMED_OUT) {
                      return Observable.error(new RuntimeException("timed out before executing run()"));
                  }
                  //更新线程状态为已开始
                  if (threadState.compareAndSet(ThreadState.NOT_USING_THREAD, ThreadState.STARTED)) {
                      HystrixCounters.incrementGlobalConcurrentThreads();
                      threadPool.markThreadExecution();
                      endCurrentThreadExecutingCommand = Hystrix.startCurrentThreadExecutingCommand(getCommandKey());
                      executionResult = executionResult.setExecutedInThread();
                      //执行hook，若异常，则直接抛出异常
                      try {
                          executionHook.onThreadStart(_cmd);
                          executionHook.onRunStart(_cmd);
                          executionHook.onExecutionStart(_cmd);
                          return getUserExecutionObservable(_cmd);
                      } catch (Throwable ex) {
                          return Observable.error(ex);
                      }
                  } else {
                      //空返回
                      return Observable.empty();
                  }
              }
          }).doOnTerminate(new Action0() {
              @Override
              public void call() {
                  //结束逻辑，省略
              }
          }).doOnUnsubscribe(new Action0() {
              @Override
              public void call() {
                  //取消订阅逻辑，省略
              }
              //从线程池中获取业务执行线程
          }).subscribeOn(threadPool.getScheduler(new Func0<Boolean>() {
              @Override
              public Boolean call() {
                  //判断是否超时
                  return properties.executionIsolationThreadInterruptOnTimeout().get() && _cmd.isCommandTimedOut.get() == TimedOutStatus.TIMED_OUT;
              }
          }));
      } else {
          //信号量模式
          //省略
      }
  }
````



> 【HystrixThreadPool】

Subscription schedule(final Action0 action)：HystrixContextScheduler是Hystrix对rx中Scheduler调度器的重写，主要为了实现在Observable未被订阅时，不执行命令，以及支持在命令执行过程中能够打断运行。在rx中，Scheduler将生成对应的Worker给Observable用于执行命令，由Worker具体负责相关执行线程的调度，ThreadPoolWorker是Hystrix自行实现的Worker，执行调度的核心方法。

````java
public Subscription schedule(final Action0 action) {
    //若无订阅，则不执行直接返回
    if (subscription.isUnsubscribed()) {
        return Subscriptions.unsubscribed();
    }
    ScheduledAction sa = new ScheduledAction(action);
    subscription.add(sa);
    sa.addParent(subscription);
    //获取线程池
    ThreadPoolExecutor executor = (ThreadPoolExecutor) threadPool.getExecutor();
    //提交执行任务
    FutureTask<?> f = (FutureTask<?>) executor.submit(sa);
    sa.add(new FutureCompleterWithConfigurableInterrupt(f, shouldInterruptThread, executor));
    return sa;
}
````


## 超时检测

Hystrix超时机制降低了第三方依赖项延迟过高对调用方的影响，使请求快速失败。主要通过延迟任务机制实现，包括注册延时任务过程和执行延时任务过程。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/0bca4ce925a4c09eb3fd3ba32c32d556.png)


当隔离策略为线程池时，主线程订阅执行结果，线程池中任务线程调用提供者服务端，同时会有定时器线程在一定时间后检测任务是否完成，若未完成则表示任务超时，抛出超时异常，并且后续任务线程的执行结果也会跳过不再发布；若已完成则表示任务在超时时间内完成执行完成，定时器检测任务结束。

当隔离策略为信号量时，主线程订阅执行结果并实际调用提供者服务端（没有任务线程），当超出指定时间，主线程仍然会执行完业务调用，然后抛出超时异常。信号量模式下超时配置有一定缺陷，不能取消在执行的调用，并不能限制主线程返回时间。

> 【AbstractCommand】

ObservableexecuteCommandAndObserve(finalAbstractCommand _cmd)：超时检测入口，执行lift(new HystrixObservableTimeoutOperator(_cmd))关联超时检测任务。

````java
private Observable<R> executeCommandAndObserve(final AbstractCommand<R> _cmd) {
    //省略
    Observable<R> execution;
    //判断是否开启超时检测
    if (properties.executionTimeoutEnabled().get()) {
        execution = executeCommandWithSpecifiedIsolation(_cmd)
                //增加超时检测操作
                .lift(new HystrixObservableTimeoutOperator<R>(_cmd));
    } else {
        //正常执行
        execution = executeCommandWithSpecifiedIsolation(_cmd);
    }
    return execution.doOnNext(markEmits)
            .doOnCompleted(markOnCompleted)
            .onErrorResumeNext(handleFallback)
            .doOnEach(setRequestContext);
}
````



> 【HystrixObservableTimeoutOperator】

Subscriber<? super R> call(final Subscriber<? super R> child)：创建检测任务，并关联延迟任务；若检测任务执行时仍未执行完成，则抛出超时异常；若已执行完成或异常，则清除检测任务。

````java
public Subscriber<? super R> call(final Subscriber<? super R> child) {
        final CompositeSubscription s = new CompositeSubscription();
        child.add(s);
        final HystrixRequestContext hystrixRequestContext = HystrixRequestContext.getContextForCurrentThread();
        //实列化监听器
        TimerListener listener = new TimerListener() {
            @Override
            public void tick() {
                //若任务未执行完成，则更新为超时
                if (originalCommand.isCommandTimedOut.compareAndSet(TimedOutStatus.NOT_EXECUTED, TimedOutStatus.TIMED_OUT)) {
                    // 上报超时失败
                    originalCommand.eventNotifier.markEvent(HystrixEventType.TIMEOUT, originalCommand.commandKey);
                    // 取消订阅
                    s.unsubscribe();
                    final HystrixContextRunnable timeoutRunnable = new HystrixContextRunnable(originalCommand.concurrencyStrategy, hystrixRequestContext, new Runnable() {                    @Override
                    public void run() {
                        child.onError(new HystrixTimeoutException());
                    }
                });
                //抛出超时异常
                timeoutRunnable.run();
            }
        }
        //超时时间配置
        @Override
        public int getIntervalTimeInMilliseconds() {
            return originalCommand.properties.executionTimeoutInMilliseconds().get();
        }
    };
    //注册监听器，关联检测任务
    final Reference<TimerListener> tl = HystrixTimer.getInstance().addTimerListener(listener);
    originalCommand.timeoutTimer.set(tl);
    Subscriber<R> parent = new Subscriber<R>() {
        @Override
        public void onCompleted() {
            if (isNotTimedOut()) {
                // 未超时情况下，任务执行完成，清除超时检测任务
                tl.clear();
                child.onCompleted();
            }
        }
        @Override
        public void onError(Throwable e) {
            if (isNotTimedOut()) {
                // 未超时情况下，任务执行异常，清除超时检测任务
                tl.clear();
                child.onError(e);
            }
        }
        @Override
        public void onNext(R v) {
                //未超时情况下，发布执行结果；超时时则直接跳过发布执行结果
            if (isNotTimedOut()) {
                child.onNext(v);
            }
        }
        //判断是否超时
        private boolean isNotTimedOut() {
            return originalCommand.isCommandTimedOut.get() == TimedOutStatus.COMPLETED ||
                    originalCommand.isCommandTimedOut.compareAndSet(TimedOutStatus.NOT_EXECUTED, TimedOutStatus.COMPLETED);
        }
    };
    s.add(parent);
    return parent;
}
````



> 【HystrixTimer】

ReferenceaddTimerListener(finalTimerListener listener)：addTimerListener通过java的定时任务服务scheduleAtFixedRate在延迟超时时间后执行。

````java
public Reference<TimerListener> addTimerListener(final TimerListener listener) {
    //初始化xian
    startThreadIfNeeded();
    //构造检测任务
    Runnable r = new Runnable() {

        @Override
        public void run() {
            try {
                listener.tick();
            } catch (Exception e) {
                logger.error("Failed while ticking TimerListener", e);
            }
        }
    };
    //延迟执行检测任务
    ScheduledFuture<?> f = executor.get().getThreadPool().scheduleAtFixedRate(r, listener.getIntervalTimeInMilliseconds(), listener.getIntervalTimeInMilliseconds(), TimeUnit.MILLISECONDS);
    return new TimerReference(listener, f);

}
````


## 降级

Hystrix降级逻辑作为兜底的策略，当出现业务执行异常、线程池或信号量已满、执行超时等情况时，会进入降级逻辑。降级逻辑中应从内存或静态逻辑获取通用返回，尽量不依赖依赖网络调用，如果未实现降级方法或降级方法中也出现异常，则业务线程中会引发异常。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/ac22e853ee0f86b74c10a20210c19131.png)

> 【AbstractCommand】

Observable getFallbackOrThrowException(finalAbstractCommand _cmd, final HystrixEventType eventType, final FailureType failureType, final String message, final Exception originalException)：首先判断是否为不可恢复异常，若是则不走降级逻辑，直接异常返回；其次判断是否能获取到降级信号量，然后走降级逻辑；当降级逻辑中也发生异常或者没有降级方法实现时，则异常返回。

````java
private Observable<R> getFallbackOrThrowException(final AbstractCommand<R> _cmd, final HystrixEventType eventType, final FailureType failureType, final String message, final Exception originalException) {
    final HystrixRequestContext requestContext = HystrixRequestContext.getContextForCurrentThread();
    long latency = System.currentTimeMillis() - executionResult.getStartTimestamp();
    executionResult = executionResult.addEvent((int) latency, eventType);
    //判断是否为不可恢复异常，如栈溢出、OOM等
    if (isUnrecoverable(originalException)) {
        logger.error("Unrecoverable Error for HystrixCommand so will throw HystrixRuntimeException and not apply fallback. ", originalException);
        Exception e = wrapWithOnErrorHook(failureType, originalException);
        //直接返回异常
        return Observable.error(new HystrixRuntimeException(failureType, this.getClass(), getLogMessagePrefix() + " " + message + " and encountered unrecoverable error.", e, null));
    } else {
        //判断为是否可恢复错误
        if (isRecoverableError(originalException)) {
            logger.warn("Recovered from java.lang.Error by serving Hystrix fallback", originalException);
        }
        //判断降级配置是否打开
        if (properties.fallbackEnabled().get()) {
          /**
            * 省略
            */
            final Func1<Throwable, Observable<R>> handleFallbackError = new Func1<Throwable, Observable<R>>() {
                @Override
                public Observable<R> call(Throwable t) {
                    Exception e = wrapWithOnErrorHook(failureType, originalException);
                    Exception fe = getExceptionFromThrowable(t);
                long latency = System.currentTimeMillis() - executionResult.getStartTimestamp();
                Exception toEmit;
                //是否是不支持操作异常，当业务中没有覆写getFallBack方法时，会抛出此异常
                if (fe instanceof UnsupportedOperationException) {
                    logger.debug("No fallback for HystrixCommand. ", fe);
                    eventNotifier.markEvent(HystrixEventType.FALLBACK_MISSING, commandKey);
                    executionResult = executionResult.addEvent((int) latency, HystrixEventType.FALLBACK_MISSING);
                    toEmit = new HystrixRuntimeException(failureType, _cmd.getClass(), getLogMessagePrefix() + " " + message + " and no fallback available.", e, fe);
                } else {
                    //执行降级逻辑时发生异常
                    logger.debug("HystrixCommand execution " + failureType.name() + " and fallback failed.", fe);
                    eventNotifier.markEvent(HystrixEventType.FALLBACK_FAILURE, commandKey);
                    executionResult = executionResult.addEvent((int) latency, HystrixEventType.FALLBACK_FAILURE);
                    toEmit = new HystrixRuntimeException(failureType, _cmd.getClass(), getLogMessagePrefix() + " " + message + " and fallback failed.", e, fe);
                }
                //判断异常是否包装
                if (shouldNotBeWrapped(originalException)) {
                    //抛出异常
                    return Observable.error(e);
                }
                //抛出异常
                return Observable.error(toEmit);
            }
        };
        //获取降级信号量
        final TryableSemaphore fallbackSemaphore = getFallbackSemaphore();
        final AtomicBoolean semaphoreHasBeenReleased = new AtomicBoolean(false);
        final Action0 singleSemaphoreRelease = new Action0() {
            @Override
            public void call() {
                if (semaphoreHasBeenReleased.compareAndSet(false, true)) {
                    fallbackSemaphore.release();
                }
            }
        };
        Observable<R> fallbackExecutionChain;
        // 尝试获取降级信号量
        if (fallbackSemaphore.tryAcquire()) {
            try {
                //判断是否定义了fallback方法
                if (isFallbackUserDefined()) {
                    executionHook.onFallbackStart(this);
                    //执行降级逻辑
                    fallbackExecutionChain = getFallbackObservable();
                } else {
                    //执行降级逻辑
                    fallbackExecutionChain = getFallbackObservable();
                }
            } catch (Throwable ex) {
                fallbackExecutionChain = Observable.error(ex);
            }
            return fallbackExecutionChain
                    .doOnEach(setRequestContext)
                    .lift(new FallbackHookApplication(_cmd))
                    .lift(new DeprecatedOnFallbackHookApplication(_cmd))
                    .doOnNext(markFallbackEmit)
                    .doOnCompleted(markFallbackCompleted)
                    .onErrorResumeNext(handleFallbackError)
                    .doOnTerminate(singleSemaphoreRelease)
                    .doOnUnsubscribe(singleSemaphoreRelease);
        } else {
            //处理降级信号量拒绝异常
           return handleFallbackRejectionByEmittingError();
        }
    } else {
        //处理降级配置关闭时异常
        return handleFallbackDisabledByEmittingError(originalException, failureType, message);
    }
}
````



> 【HystrixCommand】

R getFallback()：HystrixCommand默认抛出操作不支持异常，需要子类覆写getFalBack方法实现降级逻辑。

````java
protected R getFallback() {
    throw new UnsupportedOperationException("No fallback available.");
}
````



## 健康统计

Hystrix基于通过滑动窗口的数据统计判定服务失败占比选择性熔断，能够实现快速失败并走降级逻辑。步骤如下：

AbstractCommand执行完成后调⽤ handleCommandEnd⽅法将执行结果HystrixCommandCompletion事件发布到事件流中；

事件流通过 Observable.window()⽅法将事件按时间分组，并通过 flatMap()⽅法将事件按类型（成功、失败等）聚合成桶，形成桶流；

再将各个桶使⽤Observable.window()按窗口内桶数量聚合成滑动窗⼝数据；

将滑动窗口数据聚合成数据对象（如健康数据流、累计数据等）；

熔断器CircuitBreaker初始化时订阅健康数据流，根据健康情况修改熔断器的开关。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/ad77c1bd797f658b0f3eaaf0ca152d15.png)

> 【AbstractCommand】

void handleCommandEnd(boolean commandExecutionStarted)：在业务执行完毕后，会调用handleCommandEnd方法，在此方法中，上报执行结果executionResult，这也是健康统计的入口。

````java
private void handleCommandEnd(boolean commandExecutionStarted) {
    Reference<TimerListener> tl = timeoutTimer.get();
    if (tl != null) {
        tl.clear();
    }
long userThreadLatency = System.currentTimeMillis() - commandStartTimestamp;
executionResult = executionResult.markUserThreadCompletion((int) userThreadLatency);
//执行结果上报健康统计
if (executionResultAtTimeOfCancellation == null) {
    metrics.markCommandDone(executionResult, commandKey, threadPoolKey, commandExecutionStarted);
} else {
    metrics.markCommandDone(executionResultAtTimeOfCancellation, commandKey, threadPoolKey, commandExecutionStarted);
}

if (endCurrentThreadExecutingCommand != null) {
    endCurrentThreadExecutingCommand.call();
}
}
````





> 【BucketedRollingCounterStream】

BucketedRollingCounterStream(HystrixEventStream stream, final int numBuckets, int bucketSizeInMs,final Func2<Bucket, Event, Bucket> appendRawEventToBucket,final Func2<Output, Bucket, Output> re-duceBucket)

健康统计类HealthCountsStream的滑动窗口实现主要是在父类BucketedRollingCounterStream，首先父类BucketedCounterStream将事件流处理成桶流，BucketedRollingCounterStream处理成滑动窗口，然后由HealthCountsStream传入的reduceBucket函数处理成健康统计信息。

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/31497ea3c8aa4f9a13d1abf4b1776c6b.png)

````java
protected BucketedRollingCounterStream(HystrixEventStream<Event> stream, final int numBuckets, int bucketSizeInMs,
                                       final Func2<Bucket, Event, Bucket> appendRawEventToBucket,
                                       final Func2<Output, Bucket, Output> reduceBucket) {
    //调用父类，数据处理成桶流
    super(stream, numBuckets, bucketSizeInMs, appendRawEventToBucket);
    //根据传入的reduceBucket函数，处理滑动窗口内数据
    Func1<Observable<Bucket>, Observable<Output>> reduceWindowToSummary = new Func1<Observable<Bucket>, Observable<Output>>() {
        @Override
        public Observable<Output> call(Observable<Bucket> window) {
            return window.scan(getEmptyOutputValue(), reduceBucket).skip(numBuckets);
        }
    };
    //对父类桶流数据进行操作
    this.sourceStream = bucketedStream
    //窗口内桶数量为numBuckets，每次移动1个桶
            .window(numBuckets, 1)
            //滑动窗口内数据处理
            .flatMap(reduceWindowToSummary)
            .doOnSubscribe(new Action0() {
                @Override
                public void call() {
                    isSourceCurrentlySubscribed.set(true);
                }
            })
            .doOnUnsubscribe(new Action0() {
                @Override
                public void call() {
                    isSourceCurrentlySubscribed.set(false);
                }
            })
            .share()
            .onBackpressureDrop();
}
````





> 【HealthCounts】

HealthCounts plus(long[] eventTypeCounts)：对桶内数据按事件类型累计，生成统计数据HealthCounts；

````java
public HealthCounts plus(long[] eventTypeCounts) {
    long updatedTotalCount = totalCount;
    long updatedErrorCount = errorCount;
long successCount = eventTypeCounts[HystrixEventType.SUCCESS.ordinal()];
long failureCount = eventTypeCounts[HystrixEventType.FAILURE.ordinal()];
long timeoutCount = eventTypeCounts[HystrixEventType.TIMEOUT.ordinal()];
long threadPoolRejectedCount = eventTypeCounts[HystrixEventType.THREAD_POOL_REJECTED.ordinal()];
long semaphoreRejectedCount = eventTypeCounts[HystrixEventType.SEMAPHORE_REJECTED.ordinal()];
//总数
updatedTotalCount += (successCount + failureCount + timeoutCount + threadPoolRejectedCount + semaphoreRejectedCount);
//失败数
updatedErrorCount += (failureCount + timeoutCount + threadPoolRejectedCount + semaphoreRejectedCount);
return new HealthCounts(updatedTotalCount, updatedErrorCount);
}
````


## 本文小结

在分布式环境中，不可避免地会有许多服务的依赖项中有的失败。Hystrix作为一个库，可通过添加熔断、隔离、降级等逻辑来帮助用户控制分布式服务之间的交互，以提高系统的整体弹性。主要功能如下：

- 保护系统，控制来自访问第三方依赖项（通常是通过网络）的延迟和失败

- 阻止复杂分布式系统中的级联故障

- 快速失败并快速恢复

- 平滑降级

- 近乎实时的监控，警报和控制

Hystrix使用过程中，有一些要注意的点：

- 覆写的getFallback()方法，尽量不要有网络依赖。如果有网络依赖，建议采用多次降级，即在getFallback()内实例化 HystrixCommand，并执行Command。getFallback()尽量保证高性能返回，快速降级。

- HystrixCommand 建议采用的是线程隔离策略。

- hystrix.threadpool.default.allowMaximumSizeToDivergeFromCoreSize设置为true时，hystrix.threadpool.default.maximumSize才会生效。最大线程数需要根据业务自身情况和性能测试结果来考量，尽量初始时设置小一些，支持动态调整大小，因为它是减少负载并防止资源在延迟发生时被阻塞的主要工具。

- 信号隔离策略下，执行业务逻辑时，使用的是应用服务的父级线程（如Tomcat容器线程）。所以，一定要设置好并发量，有网络开销的调用，不建议使用该策略，容易导致容器线程排队堵塞，从而影响整个应用服务。

另外Hystrix高度依赖RxJava这个响应式函数编程框架，简单了解RxJava的使用方式，有利于理解源码逻辑。
————————————————
版权声明：本文为CSDN博主「wh柒八九」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_31960623/article/details/118882355



































