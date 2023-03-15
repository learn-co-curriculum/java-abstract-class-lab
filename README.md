# Abstract Class Lab

## Learning Goals

- Define an abstract class with an abstract method.
- Create a class hierarchy using inheritance
- Override abstract methods in subclasses

## Instructions

Fork and clone this lab.

You will implement the following class hierarchy:

- Every athlete has a jersey number.
- Football players are athletes that make touchdowns.
- Hockey players are athletes that score goals and get penalties.
- An athlete's performance rating is calculated based on the type of athlete:
  - The rating for a football player is calculated as (touchdowns * 5).
  - The rating for a hockey player is calculated as (goals * 4 - penalties * 2).

![abstract class lab uml](https://curriculum-content.s3.amazonaws.com/6677/pillars/abstract_class_lab_uml.png)

The starter code contains a class named `Athlete` with a field named `jerseyNumber`
and  concrete methods `setJerseyNumber()` and `getJerseyNumber()`.

Update the `Athlete` class to add an abstract method named `getRating()` that returns an `int`.

```java
public abstract int getRating() ;
```

Notice the `Athlete` class no longer compiles.  An abstract method must be defined in
an abstract class.   Update the class header to declare the class as abstract.
The complete `Athlete` class is shown below:

```java
public abstract class Athlete {
    private int jerseyNumber;

    public int getJerseyNumber() {
        return jerseyNumber;
    }

    public void setJerseyNumber(int jerseyNumber) {
        this.jerseyNumber = jerseyNumber;
    }

    public abstract int getRating() ;

}
```

Create a subclass of `Athlete` named `FootballPlayer`.

- Add an instance variable named `touchdowns` and get/set methods.
- Override the `getRating()` method to calculate the football player's
  rating based on the number of touchdowns (touchdowns * 5).

Create a subclass of `Athlete` named `HockeyPlayer`.

- Add two instance variables named `goals` and `penalties` and get/set methods.
- Override the `getRating()` method to calculate the hockey player's rating
  based on the number of goals and penalties (goals * 4 - penalties * 2).

Edit `Main.main` as shown:

```java
public class Main {

    public static void printAthleteInfo(Athlete athlete) {
        System.out.printf("Jersey# %d has rating of %d%n",
                athlete.getJerseyNumber(),
                athlete.getRating());
    }

    public static void main(String[] args) {

        FootballPlayer athlete1 = new FootballPlayer();
        athlete1.setJerseyNumber(22);
        athlete1.setTouchdowns(6);
        printAthleteInfo(athlete1);   //6 * 5 = 30

        FootballPlayer athlete2 = new FootballPlayer();
        athlete2.setJerseyNumber(57);
        athlete2.setTouchdowns(2);
        printAthleteInfo(athlete2);   //2 * 5 = 10

        HockeyPlayer athlete3 = new HockeyPlayer();
        athlete3.setJerseyNumber(22);
        athlete3.setGoals(5);
        athlete3.setPenalties(3);
        printAthleteInfo(athlete3);   //5 * 4 - 3 * 2 = 14

        HockeyPlayer athlete4 = new HockeyPlayer();
        athlete4.setJerseyNumber(17);
        athlete4.setGoals(1);
        printAthleteInfo(athlete4);   //1 * 4 - 0 * 2 = 4

    }
}
```

Run `Main.main` and confirm the output:

```text
Jersey# 22 has rating of 30
Jersey# 57 has rating of 10
Jersey# 22 has rating of 14
Jersey# 17 has rating of 4
```


Edit the Junit class `AthleteTest` to add the two test methods `testFootballPlayer()`
and `testHockeyPlayer()` as shown:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class AthleteTest {
    @Test
    public void testFootballPlayers() {
        FootballPlayer athlete1 = new FootballPlayer();
        athlete1.setJerseyNumber(22);
        athlete1.setTouchdowns(6);
        assertEquals(30, athlete1.getRating());

        FootballPlayer athlete2 = new FootballPlayer();
        athlete2.setJerseyNumber(57);
        athlete2.setTouchdowns(2);
        assertEquals(10, athlete2.getRating());
    }

    @Test
    public void testHockeyPlayers() {
        HockeyPlayer athlete1 = new HockeyPlayer();
        athlete1.setJerseyNumber(22);
        athlete1.setGoals(5);
        athlete1.setPenalties(3);
        assertEquals(14, athlete1.getRating());

        HockeyPlayer athlete2 = new HockeyPlayer();
        athlete2.setJerseyNumber(17);
        athlete2.setGoals(1);
        assertEquals(4, athlete2.getRating());
    }
}
```

Confirm the Junit tests pass.