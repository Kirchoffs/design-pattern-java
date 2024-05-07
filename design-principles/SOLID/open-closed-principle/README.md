# Notes
## Inheritance & Composition
### When composition is better than inheritance
Inheritance implementation:
```java
public class Character {
    public void attack() {
        System.out.println("Basic attack!");
    }

    public void defend() {
        System.out.println("Basic defend!");
    }
}

public class Warrior extends Character {
    public void attack() {
        System.out.println("Warrior slashes with a sword!");
    }
}

public class Mage extends Character {
    public void attack() {
        System.out.println("Mage casts a fireball!");
    }
}

public class Monster extends Character {
    public void attack() {
        System.out.println("Monster bites!");
    }
}
```

Composition implementation:
```java
public interface AttackBehavior {
    void attack();
}

public interface DefenseBehavior {
    void defend();
}

public interface FlyBehavior {
    void fly();
}

public class SwordAttack implements AttackBehavior {
    public void attack() {
        System.out.println("Slash with a sword!");
    }
}

public class FireballAttack implements AttackBehavior {
    public void attack() {
        System.out.println("Cast a fireball!");
    }
}

public class BasicDefense implements DefenseBehavior {
    public void defend() {
        System.out.println("Raise shield to defend!");
    }
}

public class FlyWithWings implements FlyBehavior {
    public void fly() {
        System.out.println("Flying with wings!");
    }
}

public class Character {
    private AttackBehavior attackBehavior;
    private DefenseBehavior defenseBehavior;
    private FlyBehavior flyBehavior;

    public void setAttackBehavior(AttackBehavior attackBehavior) {
        this.attackBehavior = attackBehavior;
    }

    public void setDefenseBehavior(DefenseBehavior defenseBehavior) {
        this.defenseBehavior = defenseBehavior;
    }

    public void setFlyBehavior(FlyBehavior flyBehavior) {
        this.flyBehavior = flyBehavior;
    }

    public void performAttack() {
        if (attackBehavior != null) {
            attackBehavior.attack();
        }
    }

    public void performDefense() {
        if (defenseBehavior != null) {
            defenseBehavior.defend();
        }
    }

    public void performFly() {
        if (flyBehavior != null) {
            flyBehavior.fly();
        }
    }
}
```

```java
Character warrior = new Character();
warrior.setAttackBehavior(new SwordAttack());
warrior.performAttack(); // Output: Slash with a sword!

warrior.setAttackBehavior(new FireballAttack());
warrior.performAttack(); // Output: Cast a fireball!
```

### When inheritance is better than composition
Inheritance implementation:
```java
public class Animal {
    public void breathe() {
        System.out.println("Breathing...");
    }

    public void move() {
        System.out.println("Moving...");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Cat extends Animal {
    public void meow() {
        System.out.println("Meow! Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.breathe(); // common method
        dog.move();    // common method
        dog.bark();    // specific method

        Cat cat = new Cat();
        cat.breathe(); // common method
        cat.move();    // common method
        cat.meow();    // specific method
    }
}
```

Composition implementation:
```java
public class BreathingBehavior {
    public void breathe() {
        System.out.println("Breathing...");
    }
}

public class MovingBehavior {
    public void move() {
        System.out.println("Moving...");
    }
}

public class Animal {
    private BreathingBehavior breathingBehavior;
    private MovingBehavior movingBehavior;

    public Animal(BreathingBehavior breathingBehavior, MovingBehavior movingBehavior) {
        this.breathingBehavior = breathingBehavior;
        this.movingBehavior = movingBehavior;
    }

    public void breathe() {
        breathingBehavior.breathe();
    }

    public void move() {
        movingBehavior.move();
    }
}

public class Dog extends Animal {
    public Dog(BreathingBehavior breathingBehavior, MovingBehavior movingBehavior) {
        super(breathingBehavior, movingBehavior);
    }

    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Cat extends Animal {
    public Cat(BreathingBehavior breathingBehavior, MovingBehavior movingBehavior) {
        super(breathingBehavior, movingBehavior);
    }

    public void meow() {
        System.out.println("Meow! Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        BreathingBehavior breathing = new BreathingBehavior();
        MovingBehavior moving = new MovingBehavior();

        Dog dog = new Dog(breathing, moving);
        dog.breathe();
        dog.move();   
        dog.bark();   

        Cat cat = new Cat(breathing, moving);
        cat.breathe();
        cat.move();   
        cat.meow();
    }
}
```
