# General
https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/

# Tips
https://www.youtube.com/user/SpringSourceDev/search?query=Spring+Tips

# Testing
https://www.tutorialspoint.com/mockito/
https://www.tutorialspoint.com/easymock/
http://www.baeldung.com/mockito-vs-easymock-vs-jmockit
http://www.baeldung.com/restclienttest-in-spring-boot
https://docs.spring.io/spring-security/site/docs/current/reference/html/test-mockmvc.html
https://stackoverflow.com/questions/29053974/how-to-write-a-unit-test-for-a-spring-boot-controller-endpoint
http://www.baeldung.com/introduction-to-wiremock
http://www.baeldung.com/mockito-spy


### @TestConfiguration @MockBean @SpyBean
- `✭✭✭` https://dzone.com/articles/how-to-mock-spring-bean-version-2
  * Spy on Spring Beans (Without AOP)

```java
@Profile("UserService-test")
@Configuration
public class AddressServiceTestConfiguration {
    @Bean
    @Primary
    public AddressService addressServiceSpy(AddressService addressService) {
        return Mockito.spy(addressService);
    }
}
```


```java
// The above code is in main codebase which is not good.
// A better way would be nesting the test config inside your Test class
// https://www.sylvainlemoine.com/2017/11/08/spring-boot-test-howto/
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
@AutoConfigureMockMvc
@ActiveProfiles("UserService-test")
public class SomeTest {
    @Profile("UserService-test")
    @TestConfiguration
    static class AddressServiceTestConfiguration {
        @Bean
        @Primary
        public AddressService addressServiceSpy(AddressService addressService) {
            return Mockito.spy(addressService);
        }
    }
    @Autowired
    private AddressService addressService;
}
```

```java
// The third way would be use @SpyBean(WeatherService.class) instead
// https://gooroo.io/GoorooTHINK/Article/16943/Spring-Boot-14--MockBean-and-SpyBean/24301#.WrRKw5PwZE4
```
  * The problem with @SpyBean is that Mockito cannot mock/spy final classes, anonymous classes, primitive types
    + for example, you can't spy a Spring Data Repositories such as CrudRepository. The only choice left is using @MockBean

```java
ArgumentCaptor<Person> argument = ArgumentCaptor.forClass(Person.class);
verify(mock).doSomething(argument.capture());
assertEquals("John", argument.getValue().getName());
```

- Testing Private method using powermock instead of Mockito



## Spring @Autowire on Properties vs Constructor
https://stackoverflow.com/questions/40620000/spring-autowire-on-properties-vs-constructor

## Quartz
RefundBatchJobScheduler.java

## Kafka
http://www.baeldung.com/spring-kafka

## JMX
http://docs.spring.io/spring/docs/current/spring-framework-reference/html/jmx.html
https://looksok.wordpress.com/2016/06/19/spring-jmx-manage-beans-in-runtime/

## Trend
https://www.youtube.com/playlist?list=PLTwx5YGQHdjkEgJFEojkkhgprli4Vv0Ng

## Call @Bean annotated method
https://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html#beans-java-further-information-java-config

All @Configuration classes are subclassed at startup-time with CGLIB. In the subclass, the child method checks the container first for any cached (scoped) beans before it calls the parent method and creates a new instance.

## Others
- When a spring component has a single constructor, spring will autowire the parameter of the constructor without using the @Autowire annotation
- CommandLineRunner: run some scripts during application startup
- MapStruct
- Project Lombok
- bean
  * @Primary
  * @Qualifier
  * [MapStruct](http://mapstruct.org/documentation/stable/reference/html/#decorators-with-spring) is a good example how to use @Primary and @Qualifier to implement a delegate pattern
- @RunWith(SpringRunner.class) is a alias of @RunWith(SpringJUnit4ClassRunner.class)
