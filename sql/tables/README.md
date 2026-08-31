# SQL Source Tables

This directory contains the 13 CSV files used by the SQL Server bulk-load section.

The operational CSVs `TrackingEvents.csv`, `DeliveryAttempts.csv`, `Payments.csv`, and `ProofOfDelivery.csv` are assumed/demo transactional data created to test the proposed database and query layer. Their timestamps are in 2025–2026, while the historical shipment analysis covers March 2019 to September 2020. They should not be joined to the historical KPI calculations without a matching production source.
