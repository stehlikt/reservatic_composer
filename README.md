```markdown
# Reservatic PHP API Client

Tento balíček poskytuje PHP klienta pro práci s API Reservatic.

## Požadavky

- PHP verze 8.3 nebo vyšší
- cURL rozšíření pro PHP
- JSON rozšíření pro PHP

## Instalace

Pro instalaci tohoto balíčku použijte Composer:

composer require railsformers/reservatic
```

## Použití

Zde je příklad, jak použít tento balíček:

```php
<?php

require 'vendor/autoload.php';

use Reservatic\Api;

// Vytvoření instance Reservatic
$reservatic = Api::reservatic('https://api.reservatic.com/api/vase_api', 'your_api_token', 'path/to/certificate.p12', 'certificate_password');

```

## Funkce

### `getCountries()`

Získá seznam zemí.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam zemí.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Česká republika",
        "iso_code": "CZ",
        "locale": "cs"
    }
]
```

### `getInsuranceCompanies()`

Získá seznam pojišťoven.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam pojišťoven.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Neregistrován u zdravotní pojišťovny v ČR",
        "shortcut": "Jiná",
        "code": 999
    }
]
```

### `getPhoneCodes()`

Získá seznam telefonních kódů.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam telefonních kódů.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Czech Republic",
        "position": 1,
        "value": "+420"
    }
]
```

### `getServices(int $page = null, int $per_page = null, string $q = '', string $name_cont = '')`

Získá seznam služeb.

**Parametry:**
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.
- `string $q`: (Volitelný) Hledaný výraz.
- `string $name_cont`: (Volitelný) Hledaný výraz v názvu.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam služeb.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Super service",
        "aliases": "string",
        "address": "Malostranské náměstí 1, Praha, 10000, Česká republika",
        "phone_code": "+420",
        "phone": "777888999",
        "phone_code2": "+420",
        "phone2": "777888999",
        "logo": "https://example.com/image.png",
        "ic": "12345678",
        "dic": "12345678",
        "icp": "Abc",
        "url": "https://example.com/super-service",
        "url_iframe": "https://example.com/super-service-iframe",
        "place_ids": [1, 2],
        "lat": "49.000",
        "lng": "21.000",
        "required_gdpr": true,
        "gdpr_content": "I aggree with GDPR consent",
        "external_identifier": "XA123"
    }
]
```

### `getService(int $id)`

Získá detail služby podle ID.

**Parametry:**
- `int $id`: ID služby.

**Návratová hodnota:**
- `string`: JSON string obsahující detail služby.

**Příklad:**
```json
{
    "id": 1,
    "name": "Super service",
    "aliases": "string",
    "address": "Malostranské náměstí 1, Praha, 10000, Česká republika",
    "phone_code": "+420",
    "phone": "777888999",
    "phone_code2": "+420",
    "phone2": "777888999",
    "logo": "https://example.com/image.png",
    "ic": "12345678",
    "dic": "12345678",
    "icp": "Abc",
    "url": "https://example.com/super-service",
    "url_iframe": "https://example.com/super-service-iframe",
    "place_ids": [1, 2],
    "lat": "49.000",
    "lng": "21.000",
    "required_gdpr": true,
    "gdpr_content": "I aggree with GDPR consent",
    "external_identifier": "XA123",
    "location": {
        "street": "Vřesinská 2371",
        "city": "Ostrava",
        "zip": "70800",
        "lat": 0,
        "lng": 0,
        "country_id": 1
    },
    "service_openings": [
        {
            "day": 0,
            "all_day": false,
            "closed": false,
            "no_break": false,
            "reserved_only": false,
            "time_from": "08:00",
            "time_to": "18:00",
            "break_from": "12:00",
            "break_to": "13:00"
        }
    ],
    "gopay_iframe_url": "https://example.com/payments"
}
```

### `getOperations(int $service_id, int $page = null, int $per_page = null)`

Získá seznam operací pro danou službu.

**Parametry:**
- `int $service_id`: ID služby.
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam operací.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Super operation",
        "required_fields": ["phone", "birth_cert_no", "holder_id", "date_of_birth", "address", "insurance_company", "spz"],
        "minutes": 15,
        "real_minutes": 20,
        "content": "Amazing operation",
        "has_jitsi": false,
        "anonymous_without_email": true,
        "operation_columns": [
            {
                "name": "Own Column",
                "is_required": false,
                "column_type": "options",
                "options": ["1", "2", "other"]
            }
        ],
        "create_min": 24,
        "delete_min": 24,
        "create_max": 2,
        "create_max_interval_type": "day",
        "price_without_vat": 100,
        "price_with_vat": 100,
        "price_with_vat_label": "100 Kč s DPH",
        "pay_methods": ["cash", "card", "card_in_place"],
        "currency": "czk",
        "who_pays": "free",
        "external_identifier": "XA123"
    }
]
```

### `getHolidays(int $service_id, string $from, string $to, int $user_service_id = null, int $page = null, int $per_page = null)`

Získá seznam svátků pro danou službu.

**Parametry:**
- `int $service_id`: ID služby.
- `string $from`: Počáteční datum (YYYY-MM-DD).
- `string $to`: Koncové datum (YYYY-MM-DD).
- `int $user_service_id`: (Volitelný) ID uživatelské služby.
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam svátků.

**Příklad:**
```json
[
    {
        "id": 1,
        "date": "2023-12-25",
        "description": "Christmas"
    },
    {
        "id": 2,
        "date": "2023-01-01",
        "description": "New Year"
    }
]
```

### `getServiceYears(int $service_id, int $operation_id, int $place_id = null, int $user_service_id = null)`

Získá roky pro danou službu a operaci.

**Parametry:**
- `int $service_id`: ID služby.
- `int $operation_id`: ID operace.
- `int $place_id`: (Volitelný) ID místa.
- `int $user_service_id`: (Volitelný) ID uživatelské služby.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam roků.

**Příklad:**
```json
[
    {
        "year": 2023
    },
    {
        "year": 2024
    }
]
```

### `getServiceMonths(int $service_id, int $operation_id, int $year, int $place_id = null, int $user_service_id = null)`

Získá měsíce pro danou službu, operaci a rok.

**Parametry:**
- `int $service_id`: ID služby.
- `int $operation_id`: ID operace.
- `int $year`: Rok.
- `int $place_id`: (Volitelný) ID místa.
- `int $user_service_id`: (Volitelný) ID uživatelské služby.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam měsíců.

**Příklad:**
```json
[
    {
        "month": 1
    },
    {
        "month": 2
    }
]
```

### `getServiceDays(int $service_id, int $operation_id, int $year, int $month, int $place_id = null, int $user_service_id = null)`

Získá dny pro danou službu, operaci, rok a měsíc.

**Parametry:**
- `int $service_id`: ID služby.
- `int $operation_id`: ID operace.
- `int $year`: Rok.
- `int $month`: Měsíc.
- `int $place_id`: (Volitelný) ID místa.
- `int $user_service_id`: (Volitelný) ID uživatelské služby.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam dnů.

**Příklad:**
```json
[
    {
        "day": 1
    },
    {
        "day": 2
    }
]
```

### `getServiceHours(int $service_id, int $operation_id, string $day, int $place_id = null, int $user_service_id = null)`

Získá hodiny pro danou službu, operaci a den.

**Parametry:**
- `int $service_id`: ID služby.
- `int $operation_id`: ID operace.
- `string $day`: Den (YYYY-MM-DD).
- `int $place_id`: (Volitelný) ID místa.
- `int $user_service_id`: (Volitelný) ID uživatelské služby.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam hodin.

**Příklad:**
```json
[
    {
        "label": "17:00 - 20:00",
        "free_people": 1,
        "starts_at": "2024-09-12T12:25:12+02:00",
        "place_id": 1,
        "user_service_id": 1
    }
]
```

### `getPlaces(int $service_id, int $operation_id = null, int $page = null, int $per_page = null)`

Získá seznam míst pro danou službu a operaci.

**Parametry:**
- `int $service_id`: ID služby.
- `int $operation_id`: (Volitelný) ID operace.
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam míst.

**Příklad:**
```json
[
    {
        "id": 1,
        "name": "Super kalendář",
        "service_id": 1,
        "subtext": "Text",
        "operation_ids": [1, 2],
        "external_identifier": "XA123"
    }
]
```

### `getReservations(string $from, string $to, string $status = 'kept', int $operation_id = null, int $place_id = null, int $user_service_id = null, int $user_id = null, int $external_app_id = null, string $order_by = 'starts_at', string $order_direction = 'asc', int $page = null, int $per_page = null)`

Získá seznam rezervací.

**Parametry:**
- `string $from`: Počáteční datum (YYYY-MM-DD).
- `string $to`: Koncové datum (YYYY-MM-DD).
- `string $status`: (Volitelný) Stav rezervace (výchozí: 'kept').
- `int $operation_id`: (Volitelný) ID operace.
- `int $place_id`: (Volitelný) ID místa.
- `int $user_service_id`: (Volitelný) ID uživatelské služby.
- `int $user_id`: (Volitelný) ID uživatele.
- `int $external_app_id`: (Volitelný) ID externí aplikace.
- `string $order_by`: (Volitelný) Řazení podle (výchozí: 'starts_at').
- `string $order_direction`: (Volitelný) Směr řazení (výchozí: 'asc').
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam rezervací.

**Příklad:**
```json
[
    {
        "id": 1,
        "operation_id": 2,
        "service_id": 3,
        "calendar_id": 1,
        "user_service_id": 3,
        "people": 1,
        "paid": true,
        "pay_by": "cash",
        "price": "850.0",
        "price_with_vat": 900,
        "currency": "euro",
        "operation_name": "Očkování V1",
        "operation_content": "Očkování description.",
        "operation_price": "850 euro",
        "operation_who_pays": "customer",
        "jitsi_token": "ffdc64f07e68e3647685",
        "jitsi_active": false,
        "jitsi_room_name": "Videokonference",
        "jitsi_domain": "meet.reservatic.com",
        "gopay_url": "https://gw.sandbox.gopay.com/gw/v3/token",
        "email": "john@doe.cz",
        "first_name": "John",
        "last_name": "Doe",
        "locale": "cs",
        "holder_id": "123456789",
        "phone": "777888999",
        "phone_code": "+420",
        "spz": "",
        "birth_certificate_number": "string",
        "street": "Nerudova 13",
        "city": "Praha",
        "zip": "10000",
        "country_code_alpha2": "CZ",
        "self_paying": false,
        "insurance_company_id": 1,
        "children": [
            {
                "id": 1,
                "first_name": "John",
                "last_name": "Doe",
                "date_of_birth": "2010-01-01",
                "date_of_birth_iso": "2010-01-01",
                "holder_id": 0
            }
        ],
        "reservation_columns": [
            {
                "name": "Ročník",
                "column_type": "string",
                "value": "1991",
                "values": "Red,Green,Blue"
            }
        ],
        "can_change": false,
        "can_cancel": false,
        "starts_at": "2024-09-12T12:25:12+02:00",
        "ends_at": "2024-09-12T12:40:12+02:00",
        "deleted_at": "2024-09-13T07:51:56.372Z",
        "created_at": "2024-09-12T12:25:12+02:00",
        "updated_at": "2024-09-12T12:25:12+02:00",
        "date_of_birth": "1945-01-01",
        "max_delete_at": "2024-09-13T12:25:12+02:00",
        "external_app_id": "2a4a5f29-a74b-486e-b4b9-0d6a4254bd77",
        "arrived": false,
        "pin": "1234"
    }
]
```

### `getServiceClients(int $service_id, string $q = '', string $user_first_name_cont = '', string $user_last_name_cont = '', string $user_email_cont = '', int $page = null, int $per_page = null)`

Získá seznam klientů pro danou službu.

**Parametry:**
- `int $service_id`: ID služby.
- `string $q`: (Volitelný) Hledaný výraz.
- `string $user_first_name_cont`: (Volitelný) Hledaný výraz v křestním jménu.
- `string $user_last_name_cont`: (Volitelný) Hledaný výraz v příjmení.
- `string $user_email_cont`: (Volitelný) Hledaný výraz v emailu.
- `int $page`: (Volitelný) Číslo stránky.
- `int $per_page`: (Volitelný) Počet položek na stránku.

**Návratová hodnota:**
- `string`: JSON string obsahující seznam klientů.

**Příklad:**.

```markdown

```json
[
    {
        "id": 1,
        "imported": false,
        "offline": false,
        "superclient": false,
        "blocked": false,
        "desc": false,
        "user": {
            "id": 1,
            "email": "john@doe.com",
            "first_name": "John",
            "last_name": "Doe",
            "title_front": "Mgr",
            "title_back": "Dis",
            "insurance_company_id": 1,
            "date_of_birth": "1980-01-01",
            "holder_id": "string",
            "phone": "777888999",
            "phone_code": "420",
            "locale": "cs",
            "no_emails": false,
            "avatar_url": "https://example.com/avatar.png"
        }
    }
]
```

### `postHoliday(array $data)`

Vytvoří nový svátek.

**Parametry:**
- `array $data`: Data pro vytvoření svátku.

**Návratová hodnota:**
- `string`: JSON string obsahující odpověď API.

**Příklad:**
```json
{
    "id": 1,
    "date": "2023-12-25",
    "description": "Christmas"
}
```

### `deleteHoliday(int $service_id, int $holiday_id)`

Smaže svátek podle ID.

**Parametry:**
- `int $service_id`: ID služby.
- `int $holiday_id`: ID svátku.

**Návratová hodnota:**
- `string`: JSON string obsahující odpověď API.

**Příklad:**
```json
{
    "message": "Holiday deleted successfully"
}
```

### `deleteReservation(int $id)`

Smaže rezervaci podle ID.

**Parametry:**
- `int $id`: ID rezervace.

**Návratová hodnota:**
- `string`: JSON string obsahující odpověď API.

**Příklad:**
```json
{
    "message": "Reservation deleted successfully"
}
```

### `updateReservationTime(int $id, string $time)`

Aktualizuje čas rezervace.

**Parametry:**
- `int $id`: ID rezervace.
- `string $time`: Nový čas rezervace (YYYY-MM-DDTHH:MM:SSZ).

**Návratová hodnota:**
- `string`: JSON string obsahující odpověď API.

**Příklad:**
```json
{
    "id": 1,
    "starts_at": "2023-12-25T10:00:00Z"
}
```

## Kontakt

Pokud máte nějaké dotazy nebo problémy, můžete mě kontaktovat na [podpora@reservatic.com].

