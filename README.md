<img src="https://github.com/user-attachments/assets/eea2b422-1ea0-44ac-b1b6-22070de6f363" alt="Transparent" width="100" height="100" align="right" />
<br><br>

# coma

coma is an automatic config management library for Java.
With coma you can automatically create and migrate config files without having to manually manage them in your project.

## Installation

### Maven

```xml

<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<dependency>
    <groupId>com.github.metaphoriker</groupId>
    <artifactId>coma</artifactId>
    <version>VERSION</version>
</dependency>
```

### Gradle

```groovy
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}

dependencies {
    implementation 'com.github.metaphoriker:coma:VERSION'
}
```

### Configuration

Here is a simple test configuration. The values are automatically loaded from the configuration file if it exists,
otherwise the default values are used for first generation.

```java
import de.metaphoriker.coma.BaseConfiguration;
import de.metaphoriker.coma.annotation.Key;
import de.metaphoriker.coma.annotation.Configuration;

import java.util.List;

@Configuration(fileName = "test-config", type = ConfigurationType.YAML)
class TestConfiguration extends BaseConfiguration {

    @Key(name = "test-string", description = "Test string configuration")
    private String testString = "defaultValue";

    @Key(name = "test-int", description = "Test integer configuration")
    private int testInt = 123;

    @Key(name = "test-double", description = {"Test double configuration", "Multi-line comment!"})
    private double testDouble = 123.456;

    @Key(name = "test-long", description = "Test long configuration")
    private long testLong = 1234567890L;

    @Key(name = "test-float", description = "Test float configuration")
    private float testFloat = 123.456f;

    @Key(name = "test-list", description = "Test list configuration")
    private List<String> testList = List.of("item1", "item2", "item3");

    @Key(name = "test-boolean", description = "Test boolean configuration")
    private boolean testBoolean = true;
}
```

After that you can initialize the configuration and use it like this:

```java
public static void main(String[] args) {
    TestConfiguration config = new TestConfiguration();
    config.initialize(); // loads the configuration from file or creates a new one

    System.out.println(config.getTestString());
    System.out.println(config.getTestInt());
    System.out.println(config.getTestDouble());
    System.out.println(config.getTestLong());
    System.out.println(config.getTestFloat());
    System.out.println(config.getTestList());
    System.out.println(config.isTestBoolean());
}
```

Which results in this configuration file:

```yaml
# Configuration File
# Generated by coma

# Test string configuration
test-string: "defaultValue"

# Test integer configuration
test-int: 123

# Test double configuration
# Multi-line comment!
test-double: 123.456

# Test long configuration
test-long: 1234567890

# Test float configuration
test-float: 100.0

# Test list configuration
test-list: ["item1","item2","item3"]

# Test boolean configuration
test-boolean: true
```
