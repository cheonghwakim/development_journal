### 설정 시작하기



1. pom.xml에 spring-boot-starter-web, spring-boot-starter-data-redis를 추가한다.

   ```
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

   ​

2. application.properties에 다음 내용을 설정한다.

   ```
   spring.redis.host=localhost
   spring.redis.port=6379
   ```

   spring.redis.host 옵션은 redis서버의 url 또는 ip를 설정,

   spring.redis.port는 해당 서버의 포트를 적어주시면 됩니다.  여기서 설정한 내용은 캐시 설정을 할 때 직접 불러와서 세팅을 진행하게 된다.



3. 메인 어플리케이션 클래스에 **@EnableCaching** 을 선언한다.

   ```
   @SpringBootApplication
   @EnableCaching  
   public class MongdokRedisApplication {

   	public static void main(String[] args) {
   		SpringApplication.run(MongdokRedisApplication.class, args);
   	}

   }
   ```

   해당 어노테이션을 선언하면 스프링 부트에서는 **@Cacheable**과 같은 캐싱 어노테이션의 사용을 인식하게 된다.



4. Redis와 연결을 위한 Config 파일 생성

   ```
   @Configuration
   public class RedisConfig {
     
     @Value("${spring.redis.port}")
     public int port;
     
     @Value("${spring.redis.host}")
     public String host;
     
     @Autowired
     public ObjectMapper objectMapper;
     
     @Bean
     public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
       RedisTemplate<String, Object> redisTemplate = new RedisTemplate<>();
       redisTemplate.setKeySerializer(new StringRedisSerializer());
       redisTemplate.setValueSerializer(new GenericJackson2JsonRedisSerializer());
       redisTemplate.setConnectionFactory(connectionFactory);
       return redisTemplate;
     }

     @Bean
     public RedisConnectionFactory redisConnectionFactory() {
       RedisStandaloneConfiguration redisStandaloneConfiguration = new RedisStandaloneConfiguration();
       redisStandaloneConfiguration.setHostName(host);
       redisStandaloneConfiguration.setPort(port);
       LettuceConnectionFactory connectionFactory = new LettuceConnectionFactory(redisStandaloneConfiguration);
       return connectionFactory;
     }
   }
   ```

   * RedisConnectionFactory에 사용한 LettuceConnectionFactory는 Spring boot 1.x버전대에서는 작동이 되지 않는 듯? 하위 버전에서는 JedisConnectionFactory를 사용해야 한다.



5. Spring CacheManager타입의 RedisCacheManager를 빈으로 등록한다.

   ```
   @Configuration
   public class CacheConfig {
     
     @Autowired
     RedisConnectionFactory redisConnectionFactory;
     
     @Autowired
     ObjectMapper objectMapper;
     
     @Autowired
     RedisConnectionFactory connectionFactory;
     
     
     @Bean
     public CacheManager redisCacheManager() {
       RedisCacheConfiguration redisCacheConfiguration = RedisCacheConfiguration.defaultCacheConfig()
         .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()))
         .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(new GenericJackson2JsonRedisSerializer()));
       
       RedisCacheManager redisCacheManager = RedisCacheManager.RedisCacheManagerBuilder.fromConnectionFactory(connectionFactory).cacheDefaults(redisCacheConfiguration).build();
       return redisCacheManager;
     }
     
   }
   ```

   Spring CacheManager타입의 RedisCacheManager를 빈으로 등록하면 Spring에서는 캐싱을 할 때 로컬 캐시에 저장하지 않고 redis에 저장하게 된다. 위와 같이 redisCacheManager를 등록한다. 여기까지 하면 스프링 부트에서 캐시를 사용하기 위한 준비는 끝!!





