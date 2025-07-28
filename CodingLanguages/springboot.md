# Springboot

## Getting Started

1. Go to start.spring.io in order to get a boilerplate layout for a springboot application
2. Choose maven, java, and the latest release version
3. Name your group(Ex. com.project) as well as artifact, then make sure you select the java version that is installed on your device
4. Choose Spring Web as a dependency as that's used for builing web apps
5. Choose Spring Data JPA for working with our data
6. Choose PostgreSQL Driver which allows you to work with a PostgreSQL database
7. Choose Lombok which gives you lots of boilerplate options to add to your projects
8. Once your new folder is in your work environment, connect your prepared PostgreSQL database
9. To run an application once finished and in your project directory, run **./mvnw spring-boot:run**
10. If any ports are running, do **netstat -ano | findstr :<port-number>** then **taskkill /PID <PID> /F**

## Important and common dependencies

- Spring Web: Used for building web applications, including RESTful APIs and it should be used when wanting to create web endpoints, REST APIs, or serve web pages
- Spring Data JPA: For database access using the Java Persistence API (JPA) with Spring Data. Use when wanting to interact with relational databases using repositories and entity classes
- PostgreSQL Driver: A JDBC Driver that allows your Spring Boot application to connect to a PostgreSQL database
- Lombok: A Java livrary that reduces boilerplate clode by automatically generating getters, setters, constructors, and more using annotations.
- Spring Boot DevTools: A set of tools that improve the development experience for Spring Boot apps. Enables automatic restarts, live reload, and other features that speed up development and testing.
- Spring Security: A powerful and customizable authentication and access-control framework for Spring applications. It helps you secure your application by handling user authentication, authorization, password encoding, and more.

## What is Apache Maven
- Apache Maven can be summed up to be a tool that helps programmers manage their projects and all the things they need to build their programs.
- It is used via the maven wrapper or **mvnw** which has phases
  - **clean** - Used to remove temporary directories and files
  - **default** - Where the most useful goals live
    - **compile** - Compiles your code into bytecode
    - **test** - Runs unit tests
    - **package** - Creates a jar or war file
    - **verify** - Runs checks and integration tests
  - **site** - Where documentation is generated

## Configuration
- Any additions you'd like to add to your application.properties files can be found at [https://docs.spring.io/spring-boot/appendix/application-properties/index.html](https://docs.spring.io/spring-boot/appendix/application-properties/index.html)
- This is where you can change things like the application name and the port that the application runs on

## Lombok

- **@Data** - Generates all the basic things for a class like getters, setters, toString, equals and hashcode methods, and requiredArgsConstructor
- **@NoArgsConstructor** - Basic constructor requiring no arguments
- **@AllArgsConstructor** - Constructor requiring all fields specified in class
- **@RequiredArgsConstructor** - Allows for constructor injection and only creates a constructor for final fields
  - Lets say you had a class:
  - ```java
    @RequiredArgsConstructor
    @AllArgsConstructor
    public class UserService {

      private final UserRepository userRepository;
      private String serviceName;
      private int retryCount;
    }
    ```
  - There would be a constructor created like:
  - ```java
    public UserService(UserRepository userRepository) {
      this.userRepository = userRepository;
    }
    ```
- **@Getter**
- **@Setter**


## Annotations

- **@Component**: Tells Spring to manage the class as a bean and make it available for dependency injection as well as manage its lifecycle
- **@Service**: Same functionality as @Component, and it would run the same if they were swapped, but it is just a specialization meant for the service layer
- **@Entity**: Allows a class to be mapped/created to a table in a database
- **@Table**: tag which allows you to specify your data table specific name by doing **@Table(name = "users")**
- **@Id**: tag inside your table class with your class attributes, you will have your primary key which can be identified by this
- **@GeneratedValue(strategy = GenerationType.IDENTITY)**: Usually used alongside the @Id tag that uses SQL base identity which is to auto increment our id
- **@Column(name, nullable, unique, length)**: Allows extra control over how the mapping is handled and allows you to specify attributes of a column to be mapped to your database table
- **@Enumerated(EnumType.\<type>)**: This allows you to specify the enumeration type you'll be using
- **@ManyToOne**: This allows many objects of the current class to belong to the one object that this annotation is referring to
- **JoinColumn**: Used alongside @ManyToOne an this sepecifies the column in the database that joind the two tables (the foreign key)
```java
@Entity
@Table(name="nba_stats")
public class Player {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Integer id;

  @Column(name="player_name", unique=true, nullable=false)
  private String player_name;

  private Integer player_age;

  private Double player_height;

  @Enumerated(EnumType.STRING)
  @Column(nullale = false)
  private Role role;

  public enum Role {
    PLAYER, MANAGER
  }

  @ManyToOne
  @JoinColumn(name = "team_id")
  private Team team; //This is saying that many players can belong to one team
}
```

- **@Repository**: Adding this indicates that this class is a spring data repository. Adding **extends JpaRepository<dataTable, primaryKeyType> provides CRUD operations
```java
@Repository
public interface PlayerRepository extends JpaRepository<Player, Integer> {}
```

- **@Autowired**: Injects a repository being into the service which will allow it to interact with the database
```java
@Component
public class PlayerService {
    private final PlayerRepository playerRepository;

    @Autowired
    public PlayerService(PlayerRepository playerRepository) {
        this.playerRepository = playerRepository;
    }
}
```

- **@Transactional**: Makes sure that the operation is part of a transaction meaning it maintains the data integrity during the operation
- **@RestController**: Marks a class as a spring MVC controller where every method returns a domain object instead of a view
- **@RequestMapping**: Maps web requests to handler methods within controller classes. It provides a versatile way to define how incoming HTTP requests are routed to specific methods that process them.
- **@GetMapping**: A specialized, shortcut annotation used to map HTTP GET requests to specific handler methods within a Spring controller
- **@RequestParam**: Used to extract data from the query parameters of an HTTP request URL and bind it to a method parameter in a Spring controller.
- **@PostMapping**: Used to map HTTP POST requests to specific handler methods within a Spring MVC controller.
- **@RequestBody**: When a POST request is made and information is sent by an HTTP request, @RequestBody takes the body of the HTTP request and creates the specified Java object off that information
- **@PutMapping**: Used to map HTTP PUT requests to specific handler methods within a REST controller.
- **@DeleteMapping**: Used to map HTTP DELETE requests to specific handler methods within a controller
- **@PathVariable**: Used to extract values from the URI (Uniform Resource Identifier) path and bind them to method parameters in a controller.
- **ResponseEntity\<type>(body, headers, status)**: Gives you complete control over your HTTP responses in Spring Boot REST APIs
  - Can use the static method **.ok(body)** to send an HTTP response with status 200 and the specified body message  

```java
@RestController
@RequestMapping(path = "api/v1/player")
public class PlayerController {
    private final PlayerService playerService;

    @Autowired
    public PlayerController(PlayerService playerService) {
        this.playerService = playerService;
    }

    @GetMapping
    public List<Player> getPlayers(
            @RequestParam(required=false) String team,
            @RequestParam(required=false) String name
    ) {
        if (team != null && name != null) {
            return playerService.getPlayersByName(name);
        }

        if (team != null && name == null) {
            return playerService.getPlayersFromTeam(team);
        }

        if (team == null && name != null) {
            return playerService.getPlayersFromTeam(name);
        }

        else {
            return playerService.getPlayers();
        }
    }

    @PostMapping
    public ResponseEntity<Player> addPlayer(@RequestBody Player player) {
        Player createdPlayer = playerService.addPlayer(player);
        return new ResponseEntity<>(createdPlayer, HttpStatus.CREATED);
    }

    @PutMapping
    public ResponseEntity<Player> updatePlayer(@RequestBody Player player) {
        Player resultPlayer = playerService.updatePlayer(player);
        if (resultPlayer != null) {
            return new ResponseEntity<>(resultPlayer, HttpStatus.OK);
        }
        else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }
    }

    @DeleteMapping("/{playerName}")
    public ResponseEntity<String> deletePlayer(@PathVariable String playerName) {
        playerService.deletePlayer(playerName);
        return new ResponseEntity<>("Player deleted successfully", HttpStatus.OK);
    }

}
```

- **@Configuration**: Marks the class as a source of bean definitions
- **@Bean**: Registers the method's return value as a Spring bean

## Spring Security

- When using authentication in your project, you'd first like to create a class like SecurityConfig
- Here, you should create a userDetailsService method to handle admin and normal user permissions
- Spring has a default security filter that generates temporary passwords and you normally want to override this so a separate bean should be made
- There is boilerplate code for the method to override this at [https://docs.spring.io/spring-security/reference/servlet/configuration/java.html](https://docs.spring.io/spring-security/reference/servlet/configuration/java.html) where you can search for the current implementation of securedFilterChain
- Normally want to switch out .securityMatcher("/secured/**") for **.csrf(csrf -> csrf.disable())**
- Ex.
- ```java
  @Bean
  SecurityFilterChain securityFlterChain(HttpSecurity http) throws Exception {
    return http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers(HttpMethod.POST, "/api/jobs").hasRole("ADMIN")
                .requestMatchers(HttpMethod.GET, "/api/jobs/all").permitAll()
                .requestMatchers(HttpMethod.POST, "/api/application/apply/**")
                                                        .hasRole("APPLICANT")
                .anyRequest().authenticated() // Basically a catch-all rule to require the user to be logged in for any other endpoint not explicitly specified above
            )
            .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class)
            .httpBasic(Customizer.withDefaults())
            .build();
  }
  ```

## JWT

- JWT or JSON Web Token is a way to verify a user for an entire web session without having to get credentials with each API call. When a user provides their username and password, a token is created that will be passed to each API call as their credentials
- Benefits:
  - You don't need to send your password every time which is more efficient and is safer in terms of security
  - You can build token expiration so if you'd like to auto logout after a certain amount of time, you can
  - You can store extra info in the token like roles and permissions
- General JWT Integration steps
  1. When the user logs in, the API verifies their credentials and returns the JWT token we just generated
  2. Generate JWT token which will carry the user's identity and roles
  3. For each API request, we extract and validate the token from the header
  4. Add JWT filter in the SecurityConfig before the basic Spring Auth
  5. Finally, use token to call the protected APIs and the token will go in the authorization header
- Example JwtUtil class:
```java
public static final String SECRET = "5367566859703373367639792F423F452848284D6251655468576D5A71347437";
private static final long EXPIRATION_TIME = 86400000; // 1 day (in milliseconds)

private Key getSigningKey() {
  return Keys.hmacShaKeyFor(SECRET_KEY.getBytes());
}

public String generateToken(String email) {
  return Jwts.builder()
    .setSubject(email).setIssuedAt(new Date())
    .setExpiration(new Date(System.currentTimeMillis() + EXPIRATION_TIME))
    .signWith(getSigningKey(), SignatureAlgorithm.HS256)
    .compact();
}

public String extractUsername(String token) {
    return extractClaim(token, Claims::getSubject);
}

public Date extractExpiration(String token) {
    return extractClaim(token, Claims::getExpiration);
}

public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
    final Claims claims = extractAllClaims(token);
    return claimsResolver.apply(claims);
}

private Claims extractAllClaims(String token) {
    return Jwts.parserBuilder()
            .setSigningKey(getSignKey())
            .build()
            .parseClaimsJws(token)
            .getBody();
}

private Boolean isTokenExpired(String token) {
    return extractExpiration(token).before(new Date());
}

public Boolean validateToken(String token, UserDetails userDetails) {
    final String username = extractUsername(token);
    return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
}
```

## OAuth

- Stands for Open Authorization. OAuth allows users to log in using trusted providers (like Google) without sharing their passwords with your app
- OAuth Integration steps:
  1. Register app on provider (like Google) platform which will give us a clientID and client secret
  2. When user clicks the google login, we will redirect them to the google login screen. After successful login, Google will send back an Auth code
  3. We will then send this Auth code to then ask for a token
  4. This token can then be used with the API calls and can go in the authorization header
  5. Our backend uses this token to verify with Google that the token is valid and not expired
- First, register your app on the provider site, for Google: [https://console.cloud.google.com/apis/credentials?inv=1&invt=Ab3_SA&project=sincere-apex-467319-n8](https://console.cloud.google.com/apis/credentials?inv=1&invt=Ab3_SA&project=sincere-apex-467319-n8)
- You also need to add a few things to your application.properties file
  - spring.security.oath2.client.registration.google.client-id=\<client-id>
  - spring.security.oath2.client.registration.google.client-secret=\<client-secret>
  - spring.security.oath2.client.registration.google.scope=openid,profile,email
- Add this to your pom.xml dependencies
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```

## Database Management

- There are a few lines in application.properties that need to be added:
  - **spring.datasource.url=jdbc:postgresql://localhost:5173**
  - **spring.datasource.username=<yourPostgreSQLUsername>**
  - **spring.datasource.password=<yourPostgreSQLPassword>**
  - **spring.jpa.hibernate.ddl-auto=update**: This will tell Hibernate to check for entities, compare them with existing tables, and create or update tables/columns accordingly

