# Observer Design Pattern in Java

## Overview

The **Observer Pattern** is a **behavioral design pattern** that defines a one-to-many dependency between objects. When one object (the **subject** / **observable**) changes state, all its dependents (the **observers**) are notified and updated automatically. This pattern decouples subjects from observers and is commonly used in event handling, GUI toolkits, and publish/subscribe systems.

**Concrete example:** a `NewsAgency` (subject) pushes updates to registered `NewsChannel` observers.

---

## Key Points

- One-to-many relationship: a subject notifies multiple observers.
- Observers register/unregister themselves at runtime.
- Subject knows only an abstract observer interface (loose coupling).
- Useful for event broadcasting, UI updates, messaging systems.

---

## Components (in your example)

- **Channel (Observer interface)** — `void update(Object o)`  
- **NewsChannel (Concrete Observer)** — stores and reacts to news updates.  
- **NewsAgency (Subject / Observable)** — keeps a list of `Channel` observers, and notifies them when news changes.  
- **Main (Client)** — creates subject & observers, registers observers, triggers updates.

---

## UML — Class Diagram (Mermaid)

```mermaid
classDiagram
    direction LR

    Channel <|.. NewsChannel
    NewsAgency --> Channel : maintains (List<Channel>)
    Main --> NewsAgency : uses
    Main --> NewsChannel : creates

    class Channel {
        <<interface>>
        +update(Object o)
    }

    class NewsAgency {
        -news: String
        -channels: List~Channel~
        +addObserver(channel: Channel)
        +removeObserver(channel: Channel)
        +setNews(news: String)
    }

    class NewsChannel {
        -news: String
        +update(news: Object)
        +getNews(): String
        +setNews(news: String)
    }

    class Main {
        +main()
    }
