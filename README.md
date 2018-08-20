# junit-json-params

A [Junit 5](http://junit.org/junit5/) library to provide a `@JsonFileSource`
annotation that loads data from JSON files in parameterized tests.

## Project Info
Project site: http://www.joshka.net/junit-json-params

Javadocs: http://www.joshka.net/junit-json-params/apidocs/index.html

Build Status: [![Build Status](https://travis-ci.org/joshka/junit-json-params.svg?branch=master)](https://travis-ci.org/joshka/junit-json-params)

## Maven Coordinates
```xml
<dependency>
    <groupId>net.joshka</groupId>
    <artifactId>junit-json-params</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

## Examples

```java
import net.joshka.junit.json.params;

/**
 * When passed <code>{"key":"value"}</code>, is executed a single time
 * @param object the parsed JsonObject
 */
@ParameterizedTest
@JsonFileSource(resources = "/single-object.json")
@DisplayName("provides a single object")
void singleObject(JsonObject object) {
    assertThat(object.getString("key")).isEqualTo("value");
}

/**
 * When passed <code>[{"key":"value1"},{"key","value2"}]</code>, is
 * executed once per element of the array
 * @param object the parsed JsonObject array element
 */
@ParameterizedTest
@JsonFileSource(resources = "/array-of-objects.json")
@DisplayName("provides an array of objects")
void arrayOfObjects(JsonObject object) {
    assertThat(object.getString("key")).startsWith("value");
}

/**
 * When passed <code>[1, 2]</code>, is executed once per array element
 * @param number the parsed JsonNumber for each array element
 */
@ParameterizedTest
@JsonFileSource(resources = "/array-of-numbers.json")
@DisplayName("provides an array of numbers")
void arrayOfNumbers(JsonNumber number) {
    assertThat(number.intValue()).isGreaterThan(0);
}

/**
 * When passed <code>["value1","value2"]</code>, is executed once per array
 * element
 * @param string the parsed JsonString for each array element
 */
@ParameterizedTest
@JsonFileSource(resources = "/array-of-strings.json")
@DisplayName("provides an array of strings")
void arrayOfStrings(JsonString string) {
    assertThat(string.getString()).startsWith("value");
}
```

## License
Code is under the [Apache License 2.0](LICENSE.txt)
