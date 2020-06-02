# AtomicReference

The `AtomicReference` class provides an object reference variable which can be read and written atomically. By atomic is meant that multiple threads attempting to change the same `AtomicReference` (e.g. with a compare-and-swap operation) will not make the `AtomicReference` end up in an inconsistent state. `AtomicReference` even has an advanced `compareAndSet()` method which lets you compare the reference to an expected value (reference) and if they are equal, set a new reference inside the `AtomicReference` object.

## Creating an AtomicReference

You can create an `AtomicReference` instance like this:

```
AtomicReference atomicReference = new AtomicReference();
```

If you need to create the `AtomicReference` with an initial reference, you can do so like this:

```
String initialReference = "the initially referenced string";
AtomicReference atomicReference = new AtomicReference(initialReference);
```

### Creating a Typed AtomicReference

You can use Java generics to create a typed `AtomicReference`. Here is a typed `AtomicReference` example:

```
AtomicReference<String> atomicStringReference =
    new AtomicReference<String>();
```

You can also set an initial value for a typed `AtomicReference`. Here is a typed `AtomicReference` instantiation example with an initial value:

```
String initialReference = "the initially referenced string";
AtomicReference<String> atomicStringReference =
    new AtomicReference<String>(initialReference);
```

## Getting the AtomicReference Reference

You can get the reference stored in an `AtomicReference` using the `AtomicReference`'s `get()` method. If you have an untyped `AtomicReference` then the `get()` method returns an `Object` reference. If you have a typed `AtomicReference` then `get()` returns a reference to the type you declared on the `AtomicReference` variable when you created it.

Here is first an untyped `AtomicReference` `get()` example:

```
AtomicReference atomicReference = new AtomicReference("first value referenced");

String reference = (String) atomicReference.get();
```

Notice how it is necessary to cast the reference returned by `get()` to a `String` because `get()` returns an `Object` reference when the `AtomicReference` is untyped.

Here is a typed `AtomicReference` example:

```
AtomicReference<String> atomicReference = 
     new AtomicReference<String>("first value referenced");

String reference = atomicReference.get();
```

Notice how it is no longer necessary to cast the referenced returned by `get()` because the compiler knows it will return a `String` reference.

## Setting the AtomicReference Reference

You can set the reference stored in an `AtomicReference` instance using its `set()` method. In an untyped `AtomicReference` instance the `set()` method takes an `Object` reference as parameter. In a typed `AtomicReference` the `set()` method takes whatever type as parameter you declared as its type when you declared the `AtomicReference`.

Here is an `AtomicReference` `set()` example:

```
AtomicReference atomicReference = 
     new AtomicReference();
    
atomicReference.set("New object referenced");
```

There is no difference to see in the use of the `set()` method for an untyped or typed reference. The only real difference you will experience is that the compiler will restrict the types you can set on a typed `AtomicReference`.

## Comparing and Setting the AtomicReference Reference

The `AtomicReference` class contains a useful method named `compareAndSet()`. The `compareAndSet()` method can compare the reference stored in the `AtomicReference` instance with an expected reference, and if they two references are the same (not equal as in `equals()` but same as in `==`), then a new reference can be set on the `AtomicReference` instance.

If `compareAndSet()` sets a new reference in the `AtomicReference` the `compareAndSet()` method returns `true`. Otherwise `compareAndSet()` returns `false`.

Here is an `AtomicReference` `compareAndSet()` example:

```
String initialReference = "initial value referenced";

AtomicReference<String> atomicStringReference =
    new AtomicReference<String>(initialReference);

String newReference = "new value referenced";
boolean exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);

exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);
```

This example creates a typed `AtomicReference` with an initial reference. Then it calls `comparesAndSet()` two times to compare the stored reference to the initial reference, and set a new reference if the stored reference is equal to the initial reference. The first time the two references are the same, so a new reference is set on the `AtomicReference`. The second time the stored reference is the new reference just set in the call to `compareAndSet()` before, so the stored reference is of course not equal to the initial reference. Thus, a new reference is not set on the `AtomicReference` and the `compareAndSet()` method returns `false`.