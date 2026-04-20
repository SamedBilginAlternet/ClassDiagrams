# Elevator Simulation System - Class Diagram

## Mermaid Diagram

```mermaid
classDiagram
    class Bina {
        - katSayisi: int = 12
        - asansorSayisi: int = 5
    }

    class Asansor {
        - id: int
        - mevcutKat: int
        - kapasite: int = 6
        - durum: String
        + hareket()
        + dur()
    }

    class Kat {
        - katNo: int
    }

    class Kapi {
        <<abstract>>
        - acikMi: boolean
        + ac()*
        + kapat()*
    }

    class AsansorKapisi {
        + ac()
        + kapat()
    }

    class KatKapisi {
        + ac()
        + kapat()
    }

    class Dugme {
        <<abstract>>
        - basildiMi: boolean
        + bas()*
    }

    class HedefDugmesi {
        - hedefKat: int
        + bas()
    }

    class CagriDugmesi {
        - yon: String
        + bas()
    }

    class KapiDugmesi {
        - tip: String
        + bas()
    }

    class AcilDurumDugmesi {
        + bas()
    }

    class KontrolPaneli

    class GostergeIsigi {
        - mevcutKat: int
        - yon: String
        + guncelle()
    }

    class VarisZili {
        + cal()
    }

    class Yolcu {
        - id: int
        - kalkisKati: int
        - varisKati: int
    }

    class Programlayici {
        + asansorAta()
    }

    class Simulasyon {
        + baslat()
        + durdur()
        + olayKaydet()
    }

    class Saat {
        - mevcutZaman: DateTime
        + ilerle()
        + zamanDamgasiAl()
    }

    class RastgeleSayiUreteci {
        + yolcuOlustur()
        + katBelirle()
    }

    Bina "1" *-- "5" Asansor
    Bina "1" *-- "12" Kat

    Asansor "1" *-- "1" AsansorKapisi
    Asansor "1" *-- "1" KontrolPaneli
    Asansor "1" *-- "1" GostergeIsigi
    Asansor "1" --> "0..6" Yolcu : taşır

    Kat "1" *-- "5" KatKapisi
    Kat "1" *-- "5" VarisZili
    Kat "1" *-- "5" GostergeIsigi
    Kat "1" *-- "3" CagriDugmesi

    KontrolPaneli "1" *-- "12" HedefDugmesi
    KontrolPaneli "1" *-- "2" KapiDugmesi
    KontrolPaneli "1" *-- "1" AcilDurumDugmesi

    Kapi <|-- AsansorKapisi
    Kapi <|-- KatKapisi

    Dugme <|-- HedefDugmesi
    Dugme <|-- CagriDugmesi
    Dugme <|-- KapiDugmesi
    Dugme <|-- AcilDurumDugmesi

    Simulasyon "1" *-- "1" Saat
    Simulasyon "1" *-- "1" Programlayici
    Simulasyon "1" *-- "1" RastgeleSayiUreteci
    Simulasyon "1" --> "1" Bina

    Programlayici "1" --> "5" Asansor : yönetir
```

## OOP Principles Applied

| Principle | Application |
|---|---|
| **Encapsulation** | Tüm sınıflarda `private` alanlar, `public` metodlar |
| **Inheritance** | `Kapi` → `AsansorKapisi` / `KatKapisi` — `Dugme` → 4 alt sınıf |
| **Polymorphism** | `ac()` / `kapat()` kapı tipine göre farklı davranır — `bas()` düğme tipine göre farklı davranır |
| **Abstraction** | `Kapi` ve `Dugme` abstract sınıflar, doğrudan örneklenemez |

## Architecture Notes

- `Kat` başına 5 `KatKapisi` + 5 `VarisZili` + 5 `GostergeIsigi` → her asansör boşluğu için birer tane
- `KontrolPaneli` başına 12 `HedefDugmesi` (12 kat), 2 `KapiDugmesi` (aç/kapat), 1 `AcilDurumDugmesi`
- `Simulasyon` her şeyi orkestre eder — `Saat`, `Programlayici` ve `RastgeleSayiUreteci` composition ile bağlıdır
