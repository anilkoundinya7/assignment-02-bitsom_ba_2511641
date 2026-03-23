## Database Recommendation

For a healthcare patient management system, MySQL would be my primary database recommendation. In Part 1 of this assignment, a relational schema was designed and normalization was applied, which eliminated redundancy and maintained data consistency. This is particularly important in healthcare environments where patient records, prescriptions, and billing information must remain accurate at all times. MySQL adheres to ACID properties, guaranteeing reliable transactions and preserving data integrity even when system failures occur.

In Part 2, MongoDB was implemented, where JSON documents with nested structures and arrays were created, and operations such as insertMany, find, updateOne, and indexing were performed. This highlighted MongoDB's capability in managing flexible and semi-structured data. It operates on the BASE model, which emphasizes availability and scalability while permitting eventual consistency.

With respect to the CAP theorem, MySQL prioritizes Consistency and Partition Tolerance (CP), making it a strong fit for systems that demand strict data correctness. MongoDB, on the other hand, generally favors Availability and Partition Tolerance (AP), which suits applications that need high scalability and fast query performance.

If a fraud detection module were to be incorporated, a hybrid approach would prove more effective. MySQL would handle the core transactional data, while MongoDB could be used to store and process large volumes of logs or behavioral patterns, enabling efficient anomaly detection.

To conclude, drawing from both the theoretical understanding and the hands-on implementation carried out in this assignment, MySQL is the most appropriate choice for critical healthcare operations, while MongoDB serves as a strong complement for scalable analytics and advanced feature support.