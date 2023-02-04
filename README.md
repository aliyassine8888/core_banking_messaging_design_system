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