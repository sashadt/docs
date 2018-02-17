# Online Analytics Service (OAS)

Online Analytics Service (OAS) is an Apex application which is delivered as a service in some of the DT RTS applications, for example, Omni Channel Fraud Prevention Application.  It is a Druid based system that can query in real-time on data streams from various source applications.

OAS is integrated with OAS Dashboards service which is a DataTorrent RTS Service that has been built using Apache Superset. See [OAS Dashboards Service](oas_dashboards)

OAS Dashboards performs visualization on the frontend, whereas Online Analytics Service (OAS) provides a backend for OAS Dashboards to query the expected visualization.

Both OAS and OAS Dashboards are interdependent services that provides a complete end-to-end Data Analytics solution for actionable insights into the data.

OAS is available only with _DT Premium_ license.

# Workflow of OAS

The following image depicts the workflow of OAS.

![](images/Workflow.png)

- OAS is enabled to stream-in data from Apache Kafka. Any datasource can send the applicable data for analysis into Kafka.
- The Online Analytics Service takes this real-time feed of data from Apache Kafka, computes, and makes it ready for querying.
- OAS Dashboards service can query on OAS in real time through DT gateway.

OAS can be specified as a service for an application and managed from the Services page. For more details, refer to [Services](services.md)

# Packaging OAS

Refer to [Packaging Services](services) for more details.

# Managing OAS Service

Refer to [Managing Services](services) for more details.
