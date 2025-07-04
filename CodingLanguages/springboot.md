# Springboot

## Getting Started

1. Go to start.spring.io in order to get a boilerplate layout for a springboot application
2. Choose maven, java, and 3.3.13
3. Name your group as well as artifact, then make sure you select the java version that is installed on your device
4. Choose Spring Web as a dependency as that's used for builing web apps
5. Choose Spring Data JPA for working with our data
6. Choose PostgreSQL Driver which allows you to work with a PostgreSQL database
7. Once your new folder is in your work environment, connect your prepared PostgreSQL database
8. To run an application once finished and in your project directory, run **./mvnw spring-boot:run**


## Tags

- \@Entity: Allows a class to be mapped to a table in a database
- Written below this is normally the \@Table tag which allows you to specify your data table specific name
- Inside your table class with your class attributes, you will have your primary key which can be identified with the \@Id tag
- Along with the \@Id tag goes the \@Column tag which tells springboot where to find this primary key in the PostgreSQL database
```java
@Entity
@Table(name="nba_stats")
public class Player {
  @Id
  @Column(name="id", unique=true)
  private Integer id;
  private String player_name;
  private Integer player_age;
  private Double player_height;
}
```

- \@Repository: Adding this indicates that this class is a spring data repository. Adding **extends JpaRepository<dataTable, primaryKeyType> provides CRUD operations
```java
@Repository
public interface PlayerRepository extends JpaRepository<Player, Integer> {}
```

- \@Component: Telling spring that this class should be managed by a spring container meaning spring will create an instance of this class and manage its lifecycle
- \@Autowired: Injects a repository being into the service which will allow it to interact with the database
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

- \@Transactional: Makes sure that the operation is part of a transaction meaning it maintains the data integrity during the operation
- \@RestController: Marks a class as a spring MVC controller where every method returns a domain object instead of a view
- \@RequestMapping: Maps web requests to handler methods within controller classes. It provides a versatile way to define how incoming HTTP requests are routed to specific methods that process them.
- \@GetMapping: A specialized, shortcut annotation used to map HTTP GET requests to specific handler methods within a Spring controller
- \ @RequestParam: Used to extract data from the query parameters of an HTTP request URL and bind it to a method parameter in a Spring controller.
- \@PostMapping: Used to map HTTP POST requests to specific handler methods within a Spring MVC controller.
- \@RequestBody: Used to bind the body of an HTTP request to a method parameter in a controller handler method. This annotation facilitates the automatic deserialization of the incoming request body, typically in formats like JSON or XML, into a specified Java object
- \@PutMapping: Used to map HTTP PUT requests to specific handler methods within a REST controller.
- \@DeleteMapping: Used to map HTTP DELETE requests to specific handler methods within a controller
- \@PathVariable: Used to extract values from the URI (Uniform Resource Identifier) path and bind them to method parameters in a controller.

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


