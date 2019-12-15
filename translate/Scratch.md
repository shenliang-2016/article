#### 6.1.2 使用 `JavaMailSender` 和 `MimeMessagePreparator`

本节描述另一种 `OrderManager` 的实现，它使用 `MimeMessagePreparator` 回调接口。下面的例子中，`mailSender` 属性是 `JavaMailSender` 类型，因此我们可以使用 JavaMail `MimeMessage` 类：

```java
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

import javax.mail.internet.MimeMessage;
import org.springframework.mail.MailException;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessagePreparator;

public class SimpleOrderManager implements OrderManager {

    private JavaMailSender mailSender;

    public void setMailSender(JavaMailSender mailSender) {
        this.mailSender = mailSender;
    }

    public void placeOrder(final Order order) {
        // Do the business calculations...
        // Call the collaborators to persist the order...

        MimeMessagePreparator preparator = new MimeMessagePreparator() {
            public void prepare(MimeMessage mimeMessage) throws Exception {
                mimeMessage.setRecipient(Message.RecipientType.TO,
                        new InternetAddress(order.getCustomer().getEmailAddress()));
                mimeMessage.setFrom(new InternetAddress("mail@mycompany.com"));
                mimeMessage.setText("Dear " + order.getCustomer().getFirstName() + " " +
                        order.getCustomer().getLastName() + ", thanks for your order. " +
                        "Your order number is " + order.getOrderNumber() + ".");
            }
        };

        try {
            this.mailSender.send(preparator);
        }
        catch (MailException ex) {
            // simply log it and go on...
            System.err.println(ex.getMessage());
        }
    }

}
```

> 邮件代码是一个横切关注点，很可能是能够重构进入 [custom Spring AOP aspect](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 的候选者，随后可以在 `OrderManager` 目标上合适的连接点被执行。

Spring 框架的邮件支持包含标准 JavaMail 实现。参考相关文档获取更多信息。

### 6.2 使用 JavaMail `MimeMessageHelper`

处理 JavaMail 消息时非常方便的类是 `org.springframework.mail.javamail.MimeMessageHelper`，它使您不必使用冗长的 JavaMail API。使用 `MimeMessageHelper`，创建 `MimeMessage` 非常容易，如以下示例所示：

```java
// of course you would use DI in any real-world cases
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();
MimeMessageHelper helper = new MimeMessageHelper(message);
helper.setTo("test@host.com");
helper.setText("Thank you for ordering!");

sender.send(message);
```

#### 6.2.1 发送附件和内联资源

多部分电子邮件同时允许附件和内联资源。内联资源的示例包括您要在邮件中使用但不希望显示为附件的图像或样式表。

##### 附件

以下示例显示了如何使用 `MimeMessageHelper` 发送带有单个 JPEG 图像附件的电子邮件：

```java
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();

// use the true flag to indicate you need a multipart message
MimeMessageHelper helper = new MimeMessageHelper(message, true);
helper.setTo("test@host.com");

helper.setText("Check out this image!");

// let's attach the infamous windows Sample file (this time copied to c:/)
FileSystemResource file = new FileSystemResource(new File("c:/Sample.jpg"));
helper.addAttachment("CoolImage.jpg", file);

sender.send(message);
```

##### 內联资源

以下示例显示了如何使用 `MimeMessageHelper` 发送带有嵌入式图像的电子邮件：

```java
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();

// use the true flag to indicate you need a multipart message
MimeMessageHelper helper = new MimeMessageHelper(message, true);
helper.setTo("test@host.com");

// use the true flag to indicate the text included is HTML
helper.setText("<html><body><img src='cid:identifier1234'></body></html>", true);

// let's include the infamous windows Sample file (this time copied to c:/)
FileSystemResource res = new FileSystemResource(new File("c:/Sample.jpg"));
helper.addInline("identifier1234", res);

sender.send(message);
```

> 通过使用指定的 `Content-ID` 将内联资源添加到 `MimeMessage` 中（在上例中为 `identifier1234`）。添加文本和资源的顺序非常重要。确保首先添加文本，然后添加资源。如果您正相反进行操作，则此操作无效。

