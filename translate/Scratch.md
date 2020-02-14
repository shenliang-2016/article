##### 自动配置的 JSON 测试

要测试对象 JSON 序列化和反序列化是否按预期工作，可以使用 `@JsonTest` 注解。`@JsonTest` 自动配置可用的受支持的 JSON 映射器，可以是以下库之一：

- Jackson `ObjectMapper`, 所有 `@JsonComponent` beans 和所有 Jackson `Module`s
- `Gson`
- `Jsonb`

> 可以通过 `@JsonTest` 启用的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

如果您需要配置自动配置的元素，则可以使用 `@AutoConfigureJsonTesters` 注解。

Spring Boot 包括基于 AssertJ 的助手，这些助手与 JSONAssert 和 JsonPath 库一起使用，以检查 JSON 是否按预期方式显示。`JacksonTester`，`GsonTester`，`JsonbTester` 和 `BasicJsonTester` 类可分别用于 Jackson，Gson，Jsonb 和 Strings。使用 `@JsonTest` 时，测试类上的任何帮助程序字段都可以为 `@Autowired`。以下示例显示了 Jackson 的测试类：

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.json.*;
import org.springframework.boot.test.context.*;
import org.springframework.boot.test.json.*;

import static org.assertj.core.api.Assertions.*;

@JsonTest
class MyJsonTests {

    @Autowired
    private JacksonTester<VehicleDetails> json;

    @Test
    void testSerialize() throws Exception {
        VehicleDetails details = new VehicleDetails("Honda", "Civic");
        // Assert against a `.json` file in the same package as the test
        assertThat(this.json.write(details)).isEqualToJson("expected.json");
        // Or use JSON path based assertions
        assertThat(this.json.write(details)).hasJsonPathStringValue("@.make");
        assertThat(this.json.write(details)).extractingJsonPathStringValue("@.make")
                .isEqualTo("Honda");
    }

    @Test
    void testDeserialize() throws Exception {
        String content = "{\"make\":\"Ford\",\"model\":\"Focus\"}";
        assertThat(this.json.parse(content))
                .isEqualTo(new VehicleDetails("Ford", "Focus"));
        assertThat(this.json.parseObject(content).getMake()).isEqualTo("Ford");
    }

}
```

> JSON 帮助程序类也可以直接在标准单元测试中使用。为此，如果不使用 `@JsonTest`，请在 `@Before` 方法中调用帮助程序的 `initFields` 方法。

如果您使用的是 Spring Boot 基于 AssertJ 的帮助器，以给定的 JSON 路径声明数字值，则可能无法使用 `isEqualTo`，具体取决于类型。相反，您可以使用 AssertJ 的 `satisfies` 来断言该值符合给定条件。例如，以下示例断言实际数字是与 `0.15` 差距不超过 `0.01` 的浮点值。

```java
assertThat(json.write(message))
    .extractingJsonPathNumberValue("@.test.numberValue")
    .satisfies((number) -> assertThat(number.floatValue()).isCloseTo(0.15f, within(0.01f)));
```