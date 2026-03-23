## Storage Systems

The architecture incorporates multiple storage systems, each selected to serve a specific goal effectively.

For historical patient data used in readmission prediction, a Data Warehouse (ClickHouse — OLAP) is chosen. It provides structured, cleaned, and query-optimized storage that is well-suited for running analytical queries and training machine learning models. Its pre-aggregated metrics make it efficient for generating management reports as well.

For real-time ICU vitals and streaming data, a Data Lake (Delta Lake on S3) is used. It accommodates high-volume, multi-format data including lab results, imaging scans, and sensor readings without imposing strict schema requirements. This makes it ideal for storing raw and historical data across all formats.

For enabling doctors to query patient history using plain English, a Vector Database (Pinecone) is employed. It stores embeddings of patient records, enabling semantic search and natural language queries through the NLP Query Engine powered by LLM and RAG (Retrieval-Augmented Generation).

For day-to-day transactional operations, PostgreSQL (OLTP) handles active patient records, admissions, and orders. It ensures high consistency and fast write operations required for real-time clinical workflows.

## OLTP vs OLAP Boundary

The OLTP side of this architecture includes PostgreSQL, ICU Monitoring Devices, EHR/EMR Systems, Lab and Imaging Systems, and the Hospital MIS. These systems are responsible for capturing and updating data in real time, with a focus on fast writes, accuracy, and transactional consistency.

The boundary between OLTP and OLAP begins at the ingestion layer. Apache Kafka handles real-time streaming from ICU devices, while Apache Airflow manages nightly batch ETL pipelines from EHR, lab, and MIS sources. Once data passes through this ingestion layer, it enters the analytical storage systems — the Data Lakehouse and ClickHouse — where it is transformed, aggregated, and prepared for reporting and machine learning.

The OLAP side includes the Data Lakehouse (Delta Lake on S3), ClickHouse, Vector DB (Pinecone), and the AI and processing components such as the Readmission Risk ML Model, Real-time Vitals Processor, NLP Query Engine, and Report Engine. These systems support queries, dashboards, predictions, and AI-driven insights rather than transactional operations.

## Trade-offs

One significant trade-off in this design is between real-time processing capability and overall system complexity. Supporting both batch pipelines for historical analysis and real-time streaming for ICU monitoring requires maintaining two parallel ingestion paths, which increases architectural complexity, infrastructure cost, and the effort needed for monitoring and maintenance.

However, this dual approach is necessary to satisfy both operational and analytical requirements simultaneously. A system that only supports batch processing would fail to deliver timely ICU alerts, while a purely streaming system would struggle with large-scale historical queries.

To mitigate this trade-off, a unified ingestion layer combining Apache Kafka and Apache Airflow is used. Kafka manages real-time streams while Airflow handles scheduled batch jobs, keeping both pipelines organized under a single layer. Additionally, adopting modular and independently scalable components ensures that each part of the system can be updated or scaled without disrupting the overall architecture.
