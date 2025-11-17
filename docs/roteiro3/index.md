Create a RESTful API resource `Exchange` Using FastAPI[^1] for a store.

``` mermaid
flowchart LR
    subgraph api [Trusted Layer]
        direction TB
        gateway --> account
        gateway --> auth
        account --> db@{ shape: cyl, label: "Database" }
        auth --> account
        gateway e1@==> exchange:::red
        gateway --> product
        gateway --> order
        product --> db
        order --> db
        order --> product
    end
    exchange e3@==> 3partyapi:::green@{label: "3rd-party API"}
    internet e2@==>|request| gateway
    e1@{ animate: true }
    e2@{ animate: true }
    e3@{ animate: true }
    classDef red fill:#fcc
    classDef green fill:#cfc
    click product "#product-api" "Product API"
```

## Exchange API

**link exchange:**
[https://github.com/luisebastos/exchange](https://github.com/luisebastos/exchange)


!!! info "GET /exchange/{from}/{to}"

    Get the current of a coin from one currency to another. E.g. `GET /coin/USD/EUR`.

    === "Response"

        ``` { .json .copy .select linenums='1' }
        {
            "sell": 5.2986,
            "buy": 5.2956,
            "date": "2025-11-16 19:00:00",
            "id-account": "6ed631b5-11fe-444f-83ed-fa0af1a628c6"
        }
        ```
        ```bash
        Response code: 200 (ok)
        ```
    
    === "postman"

        ![](exchange.png){width = 100%}