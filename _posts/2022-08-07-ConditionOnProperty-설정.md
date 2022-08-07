---
title: "ConditionOnProperty 설정"
categories: spring  
tags: spring java
---

## ConditionOnProperty 조건

| Property Value | havingValue="" | havingValue="true" | havingValue="false" | havingValue="foo" |
|----------------|----------------|--------------------|---------------------|-------------------|
| "true"         | yes            | yes                | no                  | no                |
| "false"        | no             | no                 | yes                 | no                |
| "foo"          | yes            | no                 | no                  | no                |

* Property Value가 `false`를 제외하고는 havingValue=""로 빈값이면 true 이다.
* Custom 설정을 만들때 false 설정보다는 true 설정을 기본 설정으로 만드는게 유리하다

## 사용자 AutoConfiguration 예제

* 아래는 Jackson Datetime의 사용자 정의 설정을 AutoConfigure로 하는 예제 이다.
* 여러개의 Condition 어노테이션이 존재하면 그 여러개의 조건에 다 맞아야 한다.
* 아래는 ObjectMapper의 Class가 존재하고 `custom.jackson.enabled=true`거나 선언이 안되어 있으면 `true`로 간주하는 것이다.
* Spring Boot 조건 확인은
  * `ConditionEvaluationReportLoggingListener` 클래스를 Debug 모드로 로그를 출력
  * 아니면 jar 실행시 arguments 옵션에 --debug 추가

```java

@Slf4j
@Configuration
@ConditionalOnClass(ObjectMapper.class)
@ConditionalOnProperty(prefix = "custom.jackson", name = "enabled", matchIfMissing = true)
@EnableConfigurationProperties(CustomJacksonProperties.class)
@AutoConfigureAfter(JacksonAutoConfiguration.class)
public class CustomJacksonAutoConfiguration {

    @Bean
    public Jackson2ObjectMapperBuilderCustomizer jackson2ObjectMapperBuilderCustomizer(HntJacksonProperties properties) {
        return builder -> {
            /**
             * Serialize LocalDateTime to 'yyyy.MM.dd HH:mm:ss'
             */
            builder.serializerByType(LocalDateTime.class, new LocalDateTimeSerializer(DateTimeFormatter.ofPattern(properties.getDateTimeFormat())));
            builder.serializerByType(LocalDate.class, new LocalDateTimeSerializer(DateTimeFormatter.ofPattern(properties.getDateFormat())));
            builder.serializerByType(LocalTime.class, new LocalDateTimeSerializer(DateTimeFormatter.ofPattern(properties.getTimeFormat())));

            /**
             * Deserialize LocalDateTime from 'yyyy.MM.dd HH:mm:ss'
             */
            builder.deserializerByType(LocalDateTime.class, new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern(properties.getDateTimeFormat())));
            builder.deserializerByType(LocalDate.class, new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern(properties.getDateFormat())));
            builder.deserializerByType(LocalTime.class, new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern(properties.getTimeFormat())));

            /**
             * 알 수 없는 ENUM 값은 NULL 로 간주
             */
            builder.featuresToEnable(DeserializationFeature.READ_UNKNOWN_ENUM_VALUES_AS_NULL);
        };
    }
}
```

## CustomJacksonProperties

```java

@Getter
@Setter
@NoArgsConstructor
@ConfigurationProperties(prefix = "custom.jackson")
public class CustomJacksonProperties {
    private boolean enabled = true;
    private String dateTimeFormat = "yyyy.MM.dd HH:mm:ss";
    private String dateFormat = "yyyy.MM.dd";
    private String timeFormat = "HH:mm:ss";
}
```

* 추가적으로 Spring boot 2.7 부터는 @AutoConfiguration 이 추가되어 AutoConfigure를 구성할때 조금더 편하다
* @AutoConfiguration에는 `@AutoConfigureBefore`, `@AutoConfigureAfter` 가 포함되어 있다.

