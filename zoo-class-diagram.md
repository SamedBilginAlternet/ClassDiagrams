# Zoo Management System - Class Diagram

## Mermaid Diagram

```mermaid
classDiagram
    class Hayvan {
        <<abstract>>
        - turAdi: String
        - agirlik: float
        - yas: int
        + getDosage()*
        + getFeedSchedule()*
    }

    class Atlar {
        <<abstract>>
        + getDosage()
        + getFeedSchedule()
    }

    class Kedigiller {
        <<abstract>>
        + getDosage()
        + getFeedSchedule()
    }

    class Kemirgenler {
        <<abstract>>
        + getDosage()
        + getFeedSchedule()
    }

    class At
    class Zebra
    class Esek

    class Kaplan
    class Aslan

    class Sican
    class Kunduz

    Hayvan <|-- Atlar
    Hayvan <|-- Kedigiller
    Hayvan <|-- Kemirgenler

    Atlar <|-- At
    Atlar <|-- Zebra
    Atlar <|-- Esek

    Kedigiller <|-- Kaplan
    Kedigiller <|-- Aslan

    Kemirgenler <|-- Sican
    Kemirgenler <|-- Kunduz
```

## Design Decisions

| Decision | Description |
|---|---|
| `Hayvan` abstract | Common attributes here, cannot be instantiated directly |
| `getDosage()` / `getFeedSchedule()` abstract | Forces subclasses to override |
| `Atlar`, `Kedigiller`, `Kemirgenler` abstract | Each group implements its own algorithm |
| Concrete classes (`At`, `Kaplan` etc.) | Inherit from group class, no override needed unless extra behavior required |

## Polymorphism Example

```java
Hayvan h = new Kaplan();
h.getFeedSchedule();  // Kedigiller algorithm runs

Hayvan h = new Zebra();
h.getFeedSchedule();  // Atlar algorithm runs
```
