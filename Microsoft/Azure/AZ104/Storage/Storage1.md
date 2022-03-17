Azure Storage includes these data services, each of which is accessed through a storage account

- Azure Containers (Blobs) - A massively scalable object store for text and binary data
- Azure Files - Managed file shares for cloud or on prem deployments
- Azure Queues - A messaging store for reliable messaging between application components
- Azure Tables - A NoSQL store for schemaless storage of structured data (now part of Azure Cosmos DB)

|Storage Account|Recommended usage|
|---------------|-----------------|
|Standard general-purpose v2| Most scenarios including Blob, File, Queue, Table, and Data Lake Storage|
|Premium block blobs|Block blob scenarios with high-transactions rates, or scenarios that use smaller objects or require consistently low storage latency|
|Premium file shares|Enterprise or high-performance file share applications|
|Premium page blobs|Premium high-performance page blob scenarios|