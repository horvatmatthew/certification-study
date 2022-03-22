Azure Storage includes these data services, each of which is accessed through a storage account

- Azure Containers (Blobs) - A massively scalable object store for text and binary data
- Azure Files - Managed file shares for cloud or on prem deployments
- Azure Queues - A messaging store for reliable messaging between application components
- Azure Tables - A NoSQL store for schemaless storage of structured data (now part of Azure Cosmos DB)

|Storage Account|Recommended usage|
|---------------|-----------------|
|Standard General-purpose v2| Most scenarios including Blob, File, Queue, Table, and Data Lake Storage|
|Standard General-purpose v1| Legacy for blobs, queues, tables, can upgrade to v2 where possible|
|Premium BlockBlobStorage|Block blob scenarios with high-transactions rates, or scenarios that use smaller objects or require consistently low storage latency|
|Premium FileStorage|Enterprise or high-performance file share applications|
|Premium page blobs|Premium high-performance page blob scenarios|
|BlobStorage|Legacy blob only storage accounts, use Gen Purpose v2 when possible, can be upgraded|

# Storage Account Performance
- Standard -> All storage accounts, best cost option, recommended for general purpose needs, Backup and disaster recovery data, media
- Premium -> Available for BlockBlob storage, FileStorage (uses SSD), GPv1 & GPv2 (unmanaged VHDs only), Interactive, Analytics, AI/ML

# Access Tiers

|Tier|Meaning|
|---|---|
|Hot|Highest Storage Cost, Lower Access Cost|
|Cold|Lower Storage Cost, Higher Access Cost, 30 Day Min Resides|
|Archive|Lowest Storage Cost, Highest Access Cost, 180 Day Min Resides|

# Replication Strategies

|Name|Defined|
|---|---|
|Local-Redundant Storage (LRS) |3 Copies in one Region in one Zone|
|Zone-Redundant Storage (ZRS) |3 Copies in one Region in 3 different Zones|
|Geo-Redundant Storage (GRS) | Like LRS 3 Copies in Primary and 3 Readonly in Secondary|
|Geo-Zone Redundant Storage (GZRS)| ZRS in Primary, LRS Readonly in Secondary|
|Read-Access Geo-Redundant Storage (RA-GRS)| Read Only without failover|
|Read-Access Geo-Zone Redundant Storage (RA-GZRS) | Read Only without failover|

|Outage Scenarioo|LRS|ZRS|GRS/RA-GRS|GZRS/RA-GZRS|
|---|---|---|---|---|
|Data Center Node Becomes Unavailable|Yes|Yes|Yes|Yes|
|Entire Data Center Becomes Unavailable|No|Yes|Yes|Yes|
|Primary Region-Wide Outage|No|No|Yes|Yes|
|Read Access in Secondary Region When Primary is Unavailable|No|No|Yes (with RA-GRS)|Yes(with Ra-GZRS)|

# Storage Account Supported Capabilities

| |Data Objects|Performance Tiers|Access Tiers|Replication Options|
|---|---|---|---|---|
|Gen Purpose v2|Blob, File, Table, Disk, Queue, Data Lake Gen 2| Standard, Premium (Disk Only)|Hot, Cool, Archive|LRS,GRS, RA-GRS, ZRS, GZRS, RA-GZRS|
|Gen Purpose v1|Blob, File, Queue, Table and Disk|Standard, Premium (Disk Only)|N/A|LRS, GRS, RA-GRS|
|BlockBlobStorage|Blob (block blobs and append blobs)|Premium|N/A|LRS, ZRS|
|FileStorage|File Only|Premium|N/A|LRS,ZRS|
|BlobStorage|Blob (block blobs and append blobs)|Standard|Hot, Cool, Archive| LRS, GRS, RA-GRS|

# Access Storage

If your storage account is named mystorageaccount, the default end points are

|Service Name|Url|
|-----|----|
|Container Service|//mystorageaccount.blob.core.windows.net|
|Table Service|//mystorageaccount.table.core.windows.net|
|Queue Service|//mystorageaccount.queue.core.windows.net|
|File Service|//mystorageaccount.file.core.windows.net|

/Container/object -> to access endpoint

# Secure Storage Endpoints

- Firewalls and Virtual Networks restrict access to the Storage Account from specific Subnets on Virtual Networks or public IPs
- Subnets and Virtual Networks must exist in the same Azure Region or Region Pair as the Storage Account

