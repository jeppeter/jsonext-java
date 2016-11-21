# jsonext
>  java json extension
  
Maven configuration:

    <dependency>
        <groupId>com.github.jeppeter</groupId>
        <artifactId>jsonext</artifactId>
        <version>1.0</version>
    </dependency>

Gradle configuration

```groovy
    compile group: 'com.github.jeppeter', name: 'jsonext', version: '1.0'
```

## parse string for json

```java
import com.github.com.jsonext.JsonExt;

public class JsonExtTest {
    public static void main(String[] args){
        JsonExt json = new JsonExt();
        boolean bret;
        String value = "";

        json.parseString("{\"name\" : \"jack\"}");
        value = json.getString("name");
        System.out.println(value);
    }
}
```
> result is
```shell
jack
```

## get more deep
```java
import com.github.com.jsonext.JsonExt;

public class JsonExtTest {
    public static void main(String[] args){
        JsonExt json = new JsonExt();
        boolean bret;
        String value = "";
        String key = "person/name";

        bret = json.parseString("{\"person\" :{ \"name\" :\"jack\"}}");
        value = json.getString("person/name");
        System.out.println(value);
    }
}
```
> result is
```shell
jack
```

## get long or object
```java
import com.github.com.jsonext.JsonExt;

public class JsonExtTest {
    public static void main(String[] args){
        JsonExt json = new JsonExt();
        boolean bret;
        String name = "";
        String key = "person/name";
        Long age;

        bret = json.parseString("{\"person\" :{ \"name\" :\"jack\",\"age\": 13}}");
        name = json.getString("person/name");
        age = json.getLong("person/age");
        System.out.println(String.format("name %s age %d",name,age));
    }
}
```
> result is
```shell
name jack age 13
```

## get keys of one simple
```java
import com.github.com.jsonext.JsonExt;

public class JsonExtTest {
    public static void main(String[] args){
        JsonExt json = new JsonExt();
        String key = "person",longkey;
        String[] keys;
        Object value;
        int i;

        bret = json.parseString("{\"person\" :{ \"name\" :\"jack\",\"age\": 13}}");
        keys = json.getKeys("person");
        for (i=0;i<keys.length;i++) {
            longkey = String.format("person/%s",keys[i]);
            value = json.getObject(longkey);
            if (value != null){
                System.out.println(String.format("%s=%s",longkey,value.toString()));
            }
        }
    }
}
```
> result is
```shell
person/name=jack
person/age=13
```
