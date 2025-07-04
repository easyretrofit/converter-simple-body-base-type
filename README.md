[![Version](https://img.shields.io/maven-central/v/io.github.easyretrofit/converter-simple-body-base-type?logo=apache-maven&style=flat-square)](https://central.sonatype.com/artifact/io.github.easyretrofit/converter-simple-body-base-type)
[![Build](https://github.com/easyretrofit/converter-simple-body-base-type/actions/workflows/build.yml/badge.svg)](https://github.com/easyretrofit/converter-simple-body-base-type/actions/workflows/build.yml/badge.svg)
[![License](https://img.shields.io/github/license/easyretrofit/converter-simple-body-base-type.svg)](http://www.apache.org/licenses/LICENSE-2.0)


# converter-base-type
Support convert java base type like String, Short, Integer, Long, Boolean, Float, Double when you project just use `easy-retrofit-adapter-simple-body` Call Adapter. 

This converter needs to be used with the specified Call Adapter, which is an [easy-retrofit-adapter-simple-body](https://github.com/easyretrofit/adapter-simple-body/blob/main/README.md)

tips: 

if the response is JSON, you need add another converter factory like `GsonConverterFactory.create()`
please keep `BaseTypeConverterFactory` in the first of the converter factory list


## Usage
Maven:
```xml
<dependency>
    <groupId>io.github.easyretrofit</groupId>
    <artifactId>converter-simple-body-base-type</artifactId>
    <version>${latest.version}</version> <!-- 替换为实际的版本号 -->
</dependency>
```

Gradle:
```groovy
implementation 'io.github.easyretrofit:converter-simple-body-base-type:${latest.version}'
```

### used with easy-retrofit

#### create a SimpleBodyCallAdapterFactoryBuilder class
```java

public class SimpleBodyCallAdapterFactoryBuilder extends BaseCallAdapterFactoryBuilder {
    @Override
    public Converter.Factory build() {
        return SimpleBodyCallAdapterFactory.create();
    }
}

public class BaseTypeConverterFactoryBuilder extends BaseConverterFactoryBuilder {
    @Override
    public Converter.Factory build() {
        return BaseTypeConverterFactory.create();
    }
}

```

#### add SimpleBodyCallAdapterFactoryBuilder and BaseTypeConverterFactoryBuilder to your RetrofitBuilder
```java
@RetrofitBuilder(baseUrl = "${app.backend.url}",
        addConverterFactory = {BaseTypeConverterFactoryBuilder.class},
        addCallAdapterFactory = {SimpleBodyCallAdapterFactoryBuilder.class})
public interface HelloApi {

}
```


### used with retrofit2
```java

Retrofit retrofit = new Retrofit.Builder().baseUrl(server.url("/"))
        .addConverterFactory(BaseTypeConverterFactory.create())
        .addCallAdapterFactory(SimpleBodyCallAdapterFactory.create())
        .build();
```


## Support base type
- String
- Short
- Integer
- Long
- Boolean
- Float
- Double
- Void

## Example
```java
    public interface MyServiceApi {

        @GET("/void")
        Void voidResponse();

        @GET("/string")
        String stringResponse();

        @GET("/long")
        Integer intResponse();

        @GET("/boolean")
        Boolean booleanResponse();

        @GET("/short")
        Short shortResponse();

        @GET("/long")
        Long longResponse();

        @GET("/float")
        Float floatResponse();

        @GET("/double")
        Double doubleResponse();


    }
```