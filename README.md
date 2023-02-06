# Core Banking Messaging Design System

## Design Constraints
* TPS & Volumes
    * 1000 TPS 
    * Large Volume of Messages
    * 30million a day
* Avoid overwheling CBS/Downstreams Systems
* Messages will contain links to APPS and Websites
* Volumes might spike at any point of time
* Systems required to be highly available (99.99%) and resilient
* Messages Consistency is important 
* Record of Messages sent is required

<br><br>
<img src="./design/messaging_system_final.drawio.svg">

## Architecture Explanation
* Core Banking Services Notifications ( Account Balance,Account Update, Payment Status, Direct Debit Setup, Mandate Management, Statement Issuance, etc.... ) will be channeled to the process layer using a "push mechanism" as raw data.

* Raw Data gets transformed into normalised data using a processor, in order to match it up with an avro schema.

* There is a possibility to create many normalised topics depending on the business use cases.

* The Kafka Sink Connector will consume all normalised topics and sink them in the database (RDBMS)

* Notification Topics will be consumed by the notification processor micro-service in order to be sent to the experience layer.

* At the experience layer level , a request authentication is required before before accessing the resources server and initiating the notification process.

* There are different type of notifications (SMS, Email, Push Notification) each will be channeled/produced into a specific kafka topic.

* The size of the Kafka Cluster and Kubernetes Cluster will/can to be determined in the NFT test/ Load test / Performance Test.

* As part of the event driven architecture, the notification consumers at the experience layer will consume kafka messages, send to the provided &  commit the offset. A retry mechanism could be implemented.

* All Notification Topics should have the customerID as a key for all the events in order to be processed by the same Partition.

* The Kafka Sink Connector will consume messages from all notifications topics and save them in the RDBMS that will be used by the CRM/CRP Team.

* A cache is required to cache the resources ( HTML, images, files, etc)

* Shadow Ledgers ( Account, Customer, Transactions) will be used to respond to all read queries in order to minimise interaction with the CBS.

* Availability & Resiliency of Kafka and the K8s cluster could be achieved using ( HPA, VPA, and other auto-scalling strategies).

* Messages will always be available in kafka (Enents log) and retention period could be configured.









