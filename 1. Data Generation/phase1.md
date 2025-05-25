**Phase 1: Synthetic Data Generation**
A dynamic Python-based data simulation engine was architected to emulate realistic, high-frequency transactional events across seven interrelated entities central to retail operations:
Customers: Profiles containing demographic attributes, contact details, and regional segmentation.
Products: Catalog of Apple SKUs including iPhones, MacBooks, Apple Watches, EarPods, and accessories with associated metadata such as brand, model, and price.
Inventory: Real-time inventory stock levels per product per store, including restocking cycles.
Sales: Simulated point-of-sale transactions linked to customer and store dimensions.
Payments: Payment records capturing method, transaction status, and timestamp.
Shipping: Fulfillment metadata including logistics provider, delivery address, ETA, and tracking status.
Stores: Geolocated store data, region tags, and operational details across Pakistani cities.

Automation Trigger: Upon accumulation of every 100 sales transactions, the system automatically compiles the corresponding entity data into structured CSV files and initiates the data ingestion process to Google Cloud Storage.
