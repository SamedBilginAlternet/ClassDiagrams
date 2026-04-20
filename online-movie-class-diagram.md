# Online Movie Sales and Rental System - Class Diagram

## Mermaid Diagram

```mermaid
classDiagram
    class Kullanici {
        - id: String
        - ad: String
        + filmListele()
        + filmSirala()
        + filmSatinAl()
        + aboneOl()
        + filmTalepEt()
    }

    class Abone {
        - kredi: float
        + krediSatinAl()
        + filmKirala()
    }

    class Film {
        - id: String
        - baslik: String
        - satisFiyati: float
        - kiraFiyati: float
        - mevcutMu: boolean
    }

    class Abonelik {
        - baslangicTarihi: Date
        - bitisTarihi: Date
    }

    class Kiralama {
        - tarih: Date
        - suresi: int
        - krediMiktari: float
    }

    class SatinAlma {
        - tarih: Date
        - tutar: float
    }

    class FilmTalebi {
        - tarih: Date
        - durum: String
    }

    class OdemeSistemi {
        + krediSatinAl()
        + odemeAl()
    }

    Kullanici <|-- Abone

    Kullanici "1" --> "0..1" Abonelik : sahiptir
    Kullanici "1" --> "0..*" SatinAlma : satın alır
    Kullanici "1" --> "0..*" FilmTalebi : talep eder

    Abone "1" --> "1" OdemeSistemi : kredi satın alır
    Abone "1" --> "0..*" Kiralama : kiralar

    SatinAlma "0..*" --> "1" Film
    Kiralama "0..*" --> "1" Film
    FilmTalebi "0..*" --> "1" Film
```

## Design Decisions

| Decision | Description |
|---|---|
| `Kullanici` → `Abone` | Kalıtım — abone, kullanıcının özel halidir |
| `filmSatinAl()` Kullanici'da | Hem normal hem abone satın alabilir |
| `filmKirala()` Abone'da | Sadece aboneler kiralayabilir |
| `filmTalepEt()` Kullanici'da | Film mevcut değilse her kullanıcı talep edebilir |
| `Kiralama.krediMiktari` | Kiralama anında hesaptan düşülen kredi miktarı kaydedilir |
| `OdemeSistemi` ayrı sınıf | Kredi satın alma işlemi bağımsız bir sistem üzerinden yürütülür |
| `Film.mevcutMu` | Filmin mevcut olup olmadığı — talep mekanizmasını tetikler |
