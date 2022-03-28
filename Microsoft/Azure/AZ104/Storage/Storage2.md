Common uses of Blob storage include
- Serving images or documents directly to a browser
- Storing files for distributed access, such as installation
- Streaming video and audio
- Storing data for backup and restore, disaster recovery, and archiving
- Storing data for analysis by an on-premises or Azure-hosted service

Blob storage offers three types of resources 
- The storage account
- Containers in the storage account
- Blobs in an container

A container provides a grouping of a set of blobs.  All blobs must be in a container.  An account can contain an unlimited number of containers.  A container can store an unlimited number of blobs.  You can create the container in the Azure portal.

Name - may contain only lowercase, numbers, and hyphens, and must begin with a letter or a number.  The name must also be between 3 and 63 characters long.

Public access level.  By default, container data is private to the account owner.
- Use Private to ensure there is no anonymous access to the container and blobs
- Use Blob to allow anonymous public read access for blobs only
- Use Container to allow anonymous public read and list access to the entire container, including the blobs

Access Tiers
- Hot Tier is optimized for frequent access of objects in the storage account.  New storage accounts are created in the Hot tier by default.
- Cool Tier is optimized for storing large amounts of data that is infrequently accessed and stored for at least 30 days.  Storing data in the Cool tier is more cost-effective, but accessing that data may be more expensive that accessing data in the Hot Tier
- Archive Tier is optimized for data that can tolerate several hours of retrieval latency and will remain in the Archive tier for at least 180 days.  The Archive tier is the most cost-effective option for storing data, but accessing that data is more expensive that accessing data in the Hot or Cool tiers.

Azure Blob storage lifecycle management offers a rich, rule-based policy for GPv2 and Blob storage accounts.  Use the policy to transition your data to the appropriate access tiers or expire at the end of the data's lifecycle.

The lifecycle management policy lets you
- Transition blobs to a cooler storage tier (hot to cool, hot to archive, or cool to archive) to optimize for performance and cost
- Delete blobs at the end of their lifecycle
- Define rules to be run once per day at the storage account level
- Apply rules to containers or a subset of blobs

24 hours to deploy lifecycle management changes

Blob Duplication Scenarios
- Minimizing latency
- Increase efficiency for compute workloads
- Optimizing data distribution
- Optimizing costs

Considerations
- Object replication requires that blob versioning is enabled on both the source and destination accounts
- Object replicatoin doesn't support blob snapshots.  Any snapshots on a blob in the source account are not replicated to the destination account
- Object replication is supported when the source and destination accounts are in the hot or cool tier.  The source and destination accounts may be in different tiers
- When you configure object replication, you create a replicatoin policy that specifies the source storage account and the destination account.  A replication policy includes one or more rules that specify a source container and a destination container and indicate which blob blobs in the source container will be replicated.
- No immutable blob support

Azure Storage offers three types of blobs (one the blob has been created, its type cannot be changed)
- Block blobs (default) -> consist of blocks of data assembled to make a blob.  Most scenarios using Blob storage employ block blobs.  Block blobs are ideal for storing text and binary data in the cloud, like files, images, and videos
- Page blobs - can be up to 8 TB in size and are most efficient for frequent read/write operations. Azure virtual machines use page blobs as OS and data disks
- Append blobs - are like block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.

There are multiple methods to upload data to blob storage, including the following methods
- AzCopy is an easy to use command line tool for Windows and Linux that copies data to and from Blob storage, across containers, or across storage accounts
- Azure Storage Data Movement Library is a .NET library for moving data between Azure Storage services.  The AzCopy utility is build with the Data Movement Library
- Azure Data Factory supports copying data to and from Blob storage by using the account key, shared access signature, service principal, or managed identities for Azure resource authentications
- Blobfuse is a virtual file system driver for Azure Blob storage. You can use blobfuse to access your existing block blob data in your Storage account through the Linux file system
- Azure Data Box Disk is a service for transferring on-premises data to Blob storage when large datasets or network constraints make uploading data over the wire unrealistic.  You can use Azure Data Box Disk to request solid-state disks (SSDS) from Microsoft.  You can then copy your data to those disks and ship them back to Microsoft to be uploaded into Blob Storage
-Azure Import/Export service provides a way to export large amounts of data from your storage account to hard drives that you provide and that Microsoft then ships back to you with your data

When using a storage account the following billing considerations apply
- Performance tiers - As the performance tier gets cooler, the per-gigabyte cost decreases
- Data Access Cost - Data access charges increase as the tier gets cooler
- Transaction Costs - the charge increases as the tier gets cooler
- Geo-Replication data transfer costs - this charge only applies to accounts with geo-replication configured, including GRS and RA-GRS
- Outbound data transfer costs - incurs billing for bandwidth usage on a per-gigabyte basis
- Changing the storage tier - changing the account storage tier from cool to hot incurs a charge equal to reading all the data existing in the storage account.  However, changing the account from hot to cool incurs a charge equal to writing all the data into the cool tier (GPv2 accounts only)