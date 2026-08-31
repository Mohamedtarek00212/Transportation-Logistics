# Transportation & Logistics Database ERD

The SQL Server model contains 13 relational tables centered on `Shipments`. The operational tables are assumed/demo tables used to validate the proposed solution and query layer; they are not presented as part of the historical shipment KPI dataset.

```mermaid
erDiagram
    Countries ||--o{ Hubs : contains
    Countries ||--o{ Customers : contains
    Hubs ||--o{ Employees : employs
    Hubs ||--o{ Couriers : assigns
    Hubs ||--o{ TrackingEvents : records
    Customers ||--o{ Shipments : sends
    Customers ||--o{ Shipments : receives
    Hubs ||--o{ Shipments : origin
    Hubs ||--o{ Shipments : destination
    ShipmentStatusLookup ||--o{ Shipments : classifies
    MaterialLookup ||--o{ Shipments : describes
    FailureReasonLookup ||--o{ Shipments : explains
    FailureReasonLookup ||--o{ DeliveryAttempts : explains
    Shipments ||--o{ Payments : receives
    Shipments ||--o{ TrackingEvents : generates
    Shipments ||--o{ DeliveryAttempts : receives
    Shipments ||--o{ ProofOfDelivery : validates
    Couriers ||--o{ DeliveryAttempts : performs

    Countries {
        INT CountryID PK
        VARCHAR CountryName
        VARCHAR Region
    }
    ShipmentStatusLookup {
        INT StatusID PK
        VARCHAR StatusName
    }
    FailureReasonLookup {
        INT ReasonID PK
        VARCHAR FailureReason
    }
    MaterialLookup {
        INT MaterialID PK
        VARCHAR MaterialName
    }
    Hubs {
        INT HubID PK
        VARCHAR HubName
        VARCHAR City
        INT CountryID FK
    }
    Customers {
        INT CustomerID PK
        VARCHAR Name
        INT CountryID FK
        VARCHAR CustomerType
    }
    Employees {
        INT EmployeeID PK
        VARCHAR Name
        INT HubID FK
        VARCHAR Role
    }
    Couriers {
        INT CourierID PK
        VARCHAR CourierName
        INT HubID FK
    }
    Shipments {
        INT ShipmentID PK
        VARCHAR TrackingNumber
        INT SenderID FK
        INT ReceiverID FK
        INT OriginHubID FK
        INT DestinationHubID FK
        INT StatusID FK
        INT MaterialID FK
        INT FinalFailureReasonID FK
    }
    Payments {
        INT PaymentID PK
        INT ShipmentID FK
        DECIMAL Amount
    }
    TrackingEvents {
        INT EventID PK
        INT ShipmentID FK
        INT HubID FK
        DATETIME EventTime
    }
    DeliveryAttempts {
        INT AttemptID PK
        INT ShipmentID FK
        INT CourierID FK
        INT FailureReasonID FK
    }
    ProofOfDelivery {
        INT PODID PK
        INT ShipmentID FK
        VARCHAR PODType
    }
```
