# University Class Diagram

## Mermaid Diagram

```mermaid
classDiagram
    class Universite
    class Siniflik
    class Ofis
    class Departman
    class Calisan
    class Profesor
    class Memur

    Universite "1" *-- "many" Siniflik
    Universite "1" *-- "many" Departman
    Universite "1" *-- "many" Calisan

    Departman "1" *-- "many" Ofis

    Calisan "many" --> "1" Ofis : çalışır

    Calisan <|-- Profesor
    Calisan <|-- Memur
```

## Relationships

| Relationship | Type | Description |
|---|---|---|
| `Universite` → `Siniflik` | Composition | Sınıflıklar üniversiteye aittir |
| `Universite` → `Departman` | Composition | Departmanlar üniversiteye aittir |
| `Universite` → `Calisan` | Composition | Çalışanlar üniversiteye aittir |
| `Departman` → `Ofis` | Composition | Ofisler bir departmana aittir |
| `Calisan` → `Ofis` | Association | Her çalışan bir ofiste çalışır |
| `Calisan` ← `Profesor` / `Memur` | Inheritance | Profesör ve Memur, Calisan'ın alt sınıflarıdır |
