# Flight and Pilot Management System - Class Diagram

## Mermaid Diagram

```mermaid
classDiagram
    class HavaYolu {
        - id: String
    }

    class UcakTipi {
        - gerekliPilotSayisi: int
    }

    class Ucak {
        - durum: String
    }

    class Ucus {
        - id: String
        - kalkisZamani: DateTime
        - inisZamani: DateTime
    }

    class Havaalani {
        - id: String
        - isim: String
    }

    class Pilot {
        - deneyimSeviyesi: String
    }

    HavaYolu "1" *-- "1..*" Ucak : sahiptir
    HavaYolu "1" o-- "1..*" Ucus : gerçekleştirir
    HavaYolu "1" *-- "1..*" Pilot : istihdam eder

    Ucak "1..*" --> "1" UcakTipi : tipinde

    Ucus "1..*" --> "1" Ucak : kullanır
    Ucus "1..*" --> "1" Havaalani : kalkar
    Ucus "1..*" --> "1" Havaalani : iner
    Ucus "1" --> "1" Pilot : pilot
    Ucus "1" --> "1" Pilot : yardımcı pilot
```

## Relationships

| Relationship | Type | Description |
|---|---|---|
| `HavaYolu` → `Ucak` | Composition | Uçaklar havayoluna aittir |
| `HavaYolu` → `Pilot` | Composition | Pilotlar havayoluna aittir |
| `HavaYolu` → `Ucus` | Aggregation | Uçuşlar havayolu tarafından gerçekleştirilir |
| `Ucak` → `UcakTipi` | Association | Her uçak bir tipe sahiptir |
| `Ucus` → `Ucak` | Association | Uçuş bir uçakla gerçekleştirilir |
| `Ucus` → `Havaalani` (×2) | Association | Kalkış ve iniş havaalanları |
| `Ucus` → `Pilot` (×2) | Association | Pilot ve yardımcı pilot |

## Design Notes

- `Ucak` ve `UcakTipi` ayrı tutuldu — aynı tipte birden fazla uçak olabilir
- `UcakTipi.gerekliPilotSayisi` ile kaç pilot gerektiği tip bazında belirlenir
- `Ucus` → `Havaalani` ilişkisi iki kez kuruldu (kalkış / iniş)
