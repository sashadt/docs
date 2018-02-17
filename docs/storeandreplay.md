# About Store and Replay Feature

You can view the outcomes of what-if scenarios by storing incoming data and then later evaluating and visualizing the same data over different rules and business logic.

Applications with the capability to store and replay can store the incoming data from Kafka input operators and then replay the stored data with a different set of rules to visualize the outcome.

The store and replay functions can be run by adding specific properties to an application configuration. To prevent potential complication, it is recommended that only one instance of the application is launched for storing data, while separate instances of the application can be launched for replaying certain time frame of the data stored by the prior application instance. The separate instances can use different configurations and rules to achieve the purpose of what-if analysis.

When the properties are specified, the outputting to the application's HDFS path is enabled.

# Enabling Data Storage

To store data, you must create an application configuration, add the applicable properties, and launch the application with this configuration.

To store incoming data, do the following:

1. Create an application configuration. Refer to, [Creating Application Configuration](application_configurations.md).
2. From the Application Configuration list, open this application configuration and add the following optional properties with their corresponding values. Though the UI displays optional properties, these properties are required for enabling the data storage for replay:

    | **Property Name** | **Value** |
    | --- | --- |
    | dt.operator.TransactionReceiver.prop.enableArchive | true |
    | dt.operator.TransactionReceiver.prop.enableReplay | false |

    **Note** : In the above example, _dt.operator.TransactionReceiver_ is the name of the Kafka input operator. Change this name to the Kafka input operator that your application uses.
3. Click **Save** and then click **Launch**.

# Creating Rules

This is optional. Refer to [Creating Rules using CEP Workbench](cep_workbench.md).

# Enabling Replay

To replay data, you must create an application configuration, add the applicable properties, apply the required rules, and launch the application with this configuration.  Using the properties, you specify the following:

- **Enable replay**: The store function is set to false and the replay is set to true.
- **SrcArchiveAppName**: Kafka time-offset mapping is read from DB related to SrcArchiveAppName. SrcArchiveAppName is the name of the separate instance of the application that store kafka topic offset in HDFS.

**Note** : Instance name and application name are different usually a different configured name of the same application.
Path is under user path **kafka-offset/{src-app-name}/{topic}**.
- **Start time/endtime**
Specify the start time and end time to begin and stop the replay.

To enable replay, do the following:

1. Create an application configuration.
2. From the Application Configuration list, open this configuration and add the following optional properties with their corresponding properties:

    | **Property Name** | **Value** |
    | --- | --- |
    | dt.operator.TransactionReceiver.prop.enableArchive | false |
    | dt.operator.TransactionReceiver.prop.enableReplay | true |
    | dt.operator.TransactionReceiver.prop.srcArchiveAppName | SrcArchiveAppName |
    | dt.operator.TransactionReceiver.prop.replayStartTime | yyyy-MM-ddTHH:mm:ssFor example: 2017-11-20T08:11:00 |
    | dt.operator.TransactionReceiver.prop.replayEndTime | yyyy-MM-ddTHH:mm:ss2017-11-20T18:11:00 |

    **Note** : In the above example,_ **dt.operator.TransactionReceiver** _is the name of the Kafka input operator. Change this name to the Kafka input operator that your application uses.
3. Click **Save** and then click **Launch**. You can view the outcome from the **Visualize** tab by importing a dashboard for the application instance.

# Visualizing Replay of Data

To visualize the replay of data after applying various rules, you can either configure the dashboards for the same application in the application configuration or import dashboards for that application where you have enabled the replay. [
