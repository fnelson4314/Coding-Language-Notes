# Springboot

## Getting Started

1. Go to start.spring.io in order to get a boilerplate layout for a springboot application
2. Choose maven, java, and 3.3.13
3. Name your group as well as artifact, then make sure you select the java version that is installed on your device
4. Choose Spring Web as a dependency as that's used for builing web apps
5. Choose Spring Data JPA for working with our data
6. Choose PostgreSQL Driver which allows you to work with a PostgreSQL database
7. Once your new folder is in your work environment, connect your prepared PostgreSQL database


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
  @Column(name="id")
  private Integer id;
  private String player_name;
  private Integer player_age;
  private Double player_height;
}
```
