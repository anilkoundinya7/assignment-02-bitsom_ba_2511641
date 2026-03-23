
# Anomaly Analysis

## Insert Anomaly

In the 'orders_flat' table, customer information, product details, sales representative data, and order records are all combined into one flat structure.

Due to this design, neither a new customer nor a new product can be added on its own.
For instance, introducing a new product (product_id = P009) requires an accompanying order_id, along with complete customer and sales representative information.

This leads to an **insert anomaly**, where adding one category of data is unnecessarily tied to unrelated categories.
This goes against the fundamental principle of keeping independent entities in separate tables.



## Update Anomaly

Columns involved: office_address, product_name

The 'office_address' column holds conflicting values for the same sales representative.
For instance, sales representative SR01 (Deepak Joshi) has the following addresses recorded across different rows:

* "Mumbai HQ, Nariman Point, Mumbai - 400021"
* "Mumbai HQ, Nariman Pt, Mumbai - 400021"

This mismatch arises because the same data is duplicated across multiple rows and updated only partially.

Likewise, the 'product_name' column is repeated across numerous rows for the same product_id.
For example, products such as Notebook and Pen Set appear across several entries.

If a product's name or price requires a change, every related row must be updated.
Missing even a few rows results in conflicting data throughout the table.

This causes an **update anomaly** as a direct consequence of redundant data storage.



## Delete Anomaly

The table consolidates all information — product, customer, and order details — within individual rows.

Removing a row that holds unique product or customer data also wipes out all information associated with it.
For instance, if product P008 (Webcam) is recorded in only one row, deleting that row permanently erases the product from the database.

This produces a **delete anomaly**, where the removal of a single record unintentionally destroys other critical data.
This problem stems from housing all entities within a single table rather than distributing them across dedicated, related tables.





# Normalization Justification

Storing all data in one table might appear convenient at first, but it introduces serious problems in practice. In the given dataset, customer records, product information, sales representative details, and order data all coexist in a single table. This results in widespread data repetition and inconsistency.

As one example, the same sales representative may have slightly varying office addresses recorded across different rows, and product details are duplicated numerous times. Any required update must be applied to multiple rows simultaneously, significantly raising the risk of errors. Additionally, registering a new product or customer without creating an order is not possible, making the overall design rigid and impractical.

Deletion also carries unintended consequences. Removing a single row can permanently eliminate important product or customer information if that data exists nowhere else in the table.

Normalization addresses all these concerns by restructuring data into dedicated tables — customers, products, sales representatives, orders, and order_items. Each table holds only the data relevant to its entity, minimizing duplication and ensuring consistency.

In summary, normalization is not an unnecessary complexity but rather an essential practice for maintaining accurate, dependable, and scalable data management.





