# Overview

Services represent global, shared, and automatically managed Docker or Apex processes. When an application is dependent on these services, these services can be configured in RTS to be launched automatically along with the application.

Thus, when launching an application, the associated services that are configured also get launched automatically.

For example:  When you launch the [Omni Channel Fraud Prevention](http://docs.datatorrent.com/omni_channel_fraud_app/) application, the following services are installed along with it:

* Online Analytics App
* Drools Workbench
* Superset Dashboards

A Service is either an  Apex application or a Docker container. DT RTS automatically manages the services based on the application dependencies. It saves the services that were added to the system for management, and the settings required to install and launch the services.

Services can be predefined in an application or configuration packages.  Users can also manually create services using the Services Management or Application Configuration Launch pages.

DT Gateway launches the services based on service descriptors.  A service descriptor is a JSON based description of the service that comes with an application package or a configuration package.  All the services are monitored by DT Gateway at regular intervals.

As individual services get started, the Gateway creates proxy connections, where the web interface of these services can be accessed using the global Gateway address. Proxy ports can be defined in the service descriptor.

You can take administrative actions to start, stop, edit or remove these services.

The following services are required by the premium applications in DT RTS:

* Online Analytics (Will be linked to the respective guide.)
* Drools Workbench (Will be linked to the respective guide.)
* [Superset](#superset)

#### Online Analytics Service

Online Analytics Service provides analytic processing of event streams from various source applications in real-time. This is an Apex application, which provides the backend query service. The visualization for this query service is provided by [Apache Superset](#superset).

For more details refer to [&lt;Online Analytics Services&gt;]()

#### Drools Workbench

Drools Workbench is the web application and repository to manage Drools assets. The Drools Workbench provides you the capability to change the application functionality by using Drools-based rules. You can create, edit, or version the rules and apply these rules on the application.

For more details refer to [&lt;Drools Workbench documentation&gt;]()

#### Superset

Superset is a rich set of data visualizations with an easy-to-use interface for exploring and visualizing data. Using the Superset services, you can create and share dashboards as well as control the data sources that must be displayed on the dashboards.

For more details refer to [&lt;Superset dashboard documentation&gt;]()

# Management

You can manage the services using the Services page. To view and manage the services, do the following:

1. Click the Settings ![](images/dtservices/cog-wheel.png) icon located on the upper most right section of the DT RTS console.
2. Select **Services**. The **Services** page is displayed with the list of installed services. You can perform the following actions:

    * [Create new service](#create_new_service)
    * [Import packaged services](#import_packaged_service)
    * [View service instance](#view_service_instance)
    * [Edit service](#edit_service)
    * [Start services](#start_services)
    * [Stop services](#stop_services)
    * [Clone service](#clone_service)
    * [Delete services](#delete_services)

<a name="crate_new_service"></a>

#### Create New Service

To create a new service, do the following:

1. Navigate to the **Services** page.
2. Click the **create new** button. The **Create Service** dialog is shown.
3. Enter the following details:

    | Item | Description |
    | ----- | ----------- |
    | Name | Specify the name of the service. This should be a unique name. For example, **druid**, **superset** etc. |
    | Description | Enter a description about the service. |
    | Type | Specify one of the following type of the service:<ul><li>**docker** - Docker container as a service.</li><li>**apex** - Apex application as a service.</li></ul>|
    | Source URL | Specify the location of the apex application image or the docker image that was used for `docker pull`. |
    | Docker Run | Specify the optional arguments provided for the `docker run` during container setup. For example `-d -p 80:80` |
    | Docker Exec | Execute the shell command inside the docker container after it is launched with `docker exec`. |
    | Apex App Name | Specify the application name in the Apex image which must be launched. |
    | Apex Launch Properties | Specify Apex launch properties. Click **Add** to add these properties. Enter the name and the corresponding value. |
    | Gateway Proxy Configuration | Gateway Proxy allows multiple service endpoints to be grouped inside a common resource path (**/proxy/services/&lt;name&gt;**) and exposed from the Gateway listen address. |
    | Proxy Address | Port or host:port to which the proxy path forwards. |
    | Proxy Request Headers | Specify headers to be added to the request when sending to the proxy destination. This is a JSON object with a key-value pair representing a header name and value pair. Click **Add** to add more headers. |
    | Proxy Response Replacements | Specify the response replacements which represents the processing that must be performed on a returned response body.<ul><li>**URL** – Matching URL to apply the text replacement logic. For example, `example.com`</li><li>**Mime** – Matching mime to apply the text replacement logic. For example, `text/html`</li><li>**String** – Specify a string to find and replace, which may contain regular expressions with match groups.</li><li>**Replace** – Specify replacement string which may contain match group variables.</li></ul>Click **Add** to add more proxy response replacements. |

4. Click **Create** button. The new service is installed. 

Sample Docker create service dialog.

![](/images/dtservices/create-service-docker.png)

Sample Apex create service dialog.

![](/images/dtservices/create-service-apex.png)

<a name="import_packaged_service"></a>

#### Import Packaged Service

1. Navigate to the **Services** page.
2. Click the **Import** button. The **Import from Packaged Services** page is displayed with the list of available packaged services in application packages.
3. Click the **Import** button of a service to be imported.
4. An **Import Packaged Service** dialog is shown.
5. Edit the applicable entries and click the **Import** button to install the service.

<a name="view_service_instance"></a>

#### View Service Instance

1. Navigate to the **Services** page.
2. Click the service name to navigate to the service instance page.
3. The following service details are displayed on the **Service Instance** page:

    | Item | Description |
    | ---- | ----------- |
    | Name | The service name |
    | TODO: List all items in this table |

<a name="edit_service"></a>

#### Edit Service

The services are automatically launched when an associated application is launched. However, you can change the settings of the services based on your requirements and restart the services.<br/>**Note**: Only **STOPPED** services can be edited.

To edit a service, do the following:

1. Navigate to the **Services** page.
2. Select a service from the service list and click the **Edit** button. The **Edit Service** dialog is shown.
3. Edit the settings and click **Save**.<br/>The new settings are saved and will be applied when the service is restarted.

**Note**: You can also edit a service on the service instance page.

<a name="start_services"></a>

#### Start Services

To start a service, do the following:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **Start** button.

**Note**: You can also start a service on the service instance page.

<a name="stop_services"></a>

#### Stop Services

To stop a service, do the following:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **Stop** button.
3. A **Stop Service** modal is shown.  Click the **Stop** button to stop the service.

**Note**: You can also stop a service on the service instance page.

<a name="clone_service"></a>

#### Clone Service

You can clone, edit, and save the service configurations as a new service. There are two methods to clone a service configuration.

Method 1:

1. On the **Services** page, select a service to clone. 
2. Click the **Copy** button.
3. Change the service name and service configurations.<br/>Service name must be different from the original service name because it must be unique.
4. Click the **Create** button.<br/>If the original service is enabled, then the new service will be installed and started.<br/>If the original service isn't enabled, then the new service will be installed, but not started.

Method 2:

1. On the Services page, select a service to clone.
2. Click the **View** button.
3. On the service instance page, click the **Copy** button.
4. Change the service name and service configurations
5. Click the **Create** button to create the new service.

<a name="delete_services"></a>

#### Delete Services

Services can be deleted for an application from the Services management page.

To stop or start the services, do the following:

1. On the DT RTS console, click the settings icon located on upper most right section of the page and select **Services**. The Services page is displayed.
2. Select a service from the services list and click the **Delete** button.
3. The delete service confirmation modal is shown.  Click the **Delete** button to confirm that you want to delete the service.

# Installation

Some applications require services which are run in the Docker containers. For such services, you must install Docker (Version 1.9.1 or greater) on your system. Services can run in Docker installed on a remote system if Docker isn't installed on the system where the Gateway is running.

During the DT RTS installation, the Docker version is automatically detected. The version and compatibility of that version with DT RTS is shown. You can optionally configure the services to run in Docker installed on a remote system.

To specify optional remote Docker, do the following:

1. On the DT RTS console, click the settings icon located on the upper most right section of the page and select **System Configuration**. The **System Configuration** page is displayed.
2. Click **Installation Wizard**.
3. In the **Welcome** page, click **Continue**
4. On the **Configuration** page, go to the **Docker** section and set the following:

    | Field | Description |
    | ----- | ----------- |
    | Docker Host | Specify the Docker host. For example,<br/>*unix:///var/run/docker.sock or http://127.0.0.1:2376* |

5. Click **Continue** and complete the Installation wizard.

# Development

When you are developing an application based on your business requirements, you can specify the services that are associated with that application and which services are required to run when an application is launched.  This can be defined in a **service.json** file which is a service descriptor. The  **\*.apa** contains the service definitions (**services.json**) file. Each of these services can be further configured with settings for your requirements.

In the **services.json** file, you must define the following top level properties:

* [Services Property](#services_property)
* [Applications Property](#applications_property)

The **services.json** file is located in the **application.apa** within the **resources** folder: **resources/resources/services.json**

In a **services.json** file, you can use parameters which are metadata variables, implicit variables, and global configuration values.

| Fields | Description |
| ------ | ----------- |
| Metadata variables | These are variables explicitly defined in the metadata section of a service and dynamically updated via APIs. For example:<pre><code>{<br/>  "name": "druid",<br/>  ...<br/>  "metadata": {<br/>    "ipaddr" : "",<br/>    "port" : 2345<br/>  }<br/>  ...<br/>}</code></pre>In this example the metadata variables can be referenced as `${druid.ipaddr}` and `${druid.port}` in parameterizable sections of a service definition. |
| Implicit variables | These are service specific variables which should not be defined in the metadata section but are implicitly resolved by the resolver. These are as follows:<ul><li>**type** - the service type, e.g. `${druid._type}`, which will resolve to "apex" because of the type property of that service definition.</li><li>**\_state** - the current state of the service, e.g. `${druid._state}` will resolve to "STOPPED" assuming that is the current state of the druid service.</li></ul> |
| Global configuration values | These are not in the context of a service but global or gateway scope. These are:<ul><li>**${GATEWAY\_CONNECT\_ADDRESSS}** - this is the GATEWAY\_CONNECT\_ADDRESS value used in many places (typically the IP address/hostname used to connect to the gateway)</li><li>**${GATEWAY\_ADMIN\_USER}** - this is the value of current unix user who launched the gateway (value of `DTGateway.SUPER_USER_CONTEXT.getUserPrincipal().getName()`)</li></ul> |

<a name="services_property"></a>

#### Services Property

Service descriptors are defined in the `services` property.  The services property is an array of JSON objects where each object defines a service.

**Service Descriptor Parameters**

| Item | Type | Description |
| ---- | ---- | ----------- |
| name | string | Service name, which should be globally unique and only include characters that HDFS file name friendly.<br/>For example: `superset-fpa`, `druid_workbench`, etc. |
| description<br/>_(Optional)_ | string | Short description about the service. |
| type | string | Services type must be one of the following values:<br/>`docker` - service is a Docker container.<br/>`apex` - service is an Apex application. |
| srcURL | string | Specify the name of the Docker image if the service is Docker based or specify the path of the Apex application package if the service is Apex based.<br/><br/>An example for docker based services: `datatorrent/superset-fpa:1.4.0`<br/><br/>An example for an Apex based services: `${.dt.gateway.artifactHubLocation}`<br/>`/ws/v1/artifacts/com.datatorrent/dt-apoxi-oas/1.4.0-SNAPSHOT/download`<br/>or `file:///path/to/apppackage.apa` |
| docker<br/>_(Optional)_ | json | Specify the Docker details for he service.<br/>**Note**: This property is required if the service type is `docker`. |
| apex<br/>_(Optional)_ | json | Specify the Apex details for the service.<br/>**Note**: This property is required if the service type is `apex`. |
| proxy<br/>_(Optional)_ | json | Specify the proxy settings for the service. |

**Docker Details**

| Item | Type | Description |
| ---- | ---- | ----------- | 
| run | string | Specify the Docker run command details.<br/>For example: `--add-host druid_cluster:<GATEWAY_IP> -e OAS=fpa-online-analytics-service -e PORT=9090 -p 28088:8088` |
| exec | string | Specify the Docker shell command to execute after the Docker service is started.<br/>For example: `nginx -t -c ~/mynginx.conf` |

**Apex Details**

| Item | Type | Description |
| ---- | ---- | ----------- | 
| appName | string | Specify the Apex application in the APA to launch.<br/>For example: `OA` |
| launchArgs<br/>_(Optional)_ | json | Arguments to use during the launching of the Apex service.<br/>For example:<pre><code>{</br>  "kafkaBrokers": "localhost:9092",</br>  "kafkaTopic": "analytics"<br/>}</code></pre> |

**Proxy Settings**

| Item | Type | Description |
| ---- | ---- | ----------- | 
| address<br/>_(Optional)_ | string | Host:port to which the proxy path forwards to.<br/>For example: `localhost:28088` |
| requestHeaders<br/>_(Optional)_ | json | Headers to be added to the request made by the Gateway to the proxy destination. |
| replaceStrings<br/>_(Optional)_ | [json] | Definitions that represents text replacement processing to be performed on the response body by the Gateway proxy.  Regular expression is supported as described in the [Java Regex Pattern Class](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html), which includes capturing group and back references. |

**Replace Strings Details**

| Item | Type | Description |
| ---- | ---- | ----------- | 
| matchMime<br/>_(Optional)_ | string | Process only for this mime-type.<br/>For example: `text/html` |
| matchUrl<br/>_(Optional)_ | string | Process only when the URL matches this regular expression pattern.<br/>For example: `acct*` |
| matchText | string | Text to be matched in the response body.<br/>For example: `href=\"/static/` |
| replaceText<br/>_(Optional, default: '')_ | string | Text that replaces the matched-text.<br/>For example: `href=\"/proxy/services/superset-fraud-app/static/` |

Example 1:

<pre><code>{
  "matchMime": "text/html",
  "matchUrl": ".*\.html",
  "matchText": "href=\"/static/",
  "replaceText": "href=\"/proxy/services/superset-fraud-app/static/"
}</code></pre>

The above example tells the Gateway proxy to process request URLs ending with `.html` and the response header mime-type equals `text/html`.  Once the URL and mime-type are a match, then the response body is transformed by replacing every occurrence of `href="/static/` with `href="/proxy/services/superset-fraud-app/static/`.

Example 2:

<pre><code>{
  "matchMime": "text/html",
  "matchUrl": ".*",
  "matchText": "num=([0-9]*)",
  "replaceText": "NUM=\"$1\""
}</code></pre>

The above example tells the Gateway to process requests where the response header mime-type equals `text/html`.  Once the mime-type is a match, then the response body is transformed by replacing every occurrence of `num=one or more digits` with `NUM="same digits"`.  For example: `num=25` becomes `NUM="25"`, `num=100` becomes `NUM="100"`, etc.

**Note**: The matchUrl in this case will match any URL so it could have been omitted.

<a name="applications_property"></a>

#### Applications Property

Applications depending on services are defined in the `applications` property.  

**Applications Parameters**

| Item | Type | Description |
| ---- | ---- | ----------- |
| name | string | Apex application name, which exists in the current APA package. |
| requiredServices | [json] | List of services in which this application depends on.  If one of the services depends on other services, transitive service dependencies do not need to be specified explicitly. |

`requiredServices` is an array of JSON objects where each object defines a service the application depends on.

**Required Services Parameters**

| Item | Type | Description |
| ---- | ---- | ----------- |
| name | string | The service name this application depends on. |
| requiredBeforeLaunch<br/><br/>_(Optional, default: false)_ | boolean | If this property is set to true, then the application cannot be launched until this service is started. |
| transient<br/><br/>_(Optional, default: false)_ | boolean | If this property is set to true, then it is deleted when the application is killed or shutdown. |

#### Sample Services File

Following is an example of the **services.json** file.

<pre><code>{
  "services": [
    {
      "name": "superset-service",
      "description": "Superset application dashboard service.",
      "type": "docker",
      "srcUrl": "johnsmith/superset:1.0.0",
      "docker": {
        "run": "--add-host cluster:<CLUSTER_IP> -e PORT=9090 -p 28088:8088"
      },
      "proxy": {
        "address": "localhost:28088",
        "followRedirect": false,
        "requestHeaders": {
          "X_PROXY_REMOTE_USER": "admin"
        },
        "replaceStrings": [
          {
            "matchMime": ".*text/html.*",
            "matchUrl": ".*",
            "matchText": "href=\"/",
            "replaceText": "href=\"/proxy/services/superset/"
          },
          {
            "matchMime": ".*application/javascript.*",
            "matchUrl": ".*.entry.js",
            "matchText": "\"/superset/",
            "replaceText": "\"/proxy/services/superset/superset/"
          }
        ]
      }
    },
    {
      "name": "drools-workbench",
      "description": "Drools Workbench is the web application and repository to govern Drools assets.",
      "type": "docker",
      "srcUrl": "jshnsmith/drools-workbench:1.0.0",
      "docker": {
        "run": "-d -p 18080:8080 -p 18001:8001"
      },
      "proxy": {
        "address": "localhost:18080/drools-wb",
        "followRedirect": false
      }
    },
    {
      "name": "online-analytics-service",
      "description": "Online Analytics Service.",
      "type": "apex",
      "proxy": {
        "address": "${QueryIP}:${QueryPort}"
      },
      "srcUrl": "${dt.gateway.artifactHubLocation}/ws/v1/artifacts/dt-apoxi-oas/1.4.0/download",
      "apex": {
        "appName": "Online-Analytics-Service",
        "launchArgs": {
          "apex.app-param.kafkaBrokers": "localhost:9092",
          "apex.app-param.kafkaTopic": "analytics"
        }
      }
    }
  ],
  "applications": [
    {
      "name": "MyApexApplication",
      "requiredServices": [
        {
          "name": "online-analytics-service",
          "requiredBeforeLaunch": "true"
        },
        {
          "name": "superset-fpa"
        },
        {
          "name": "drools-workbench"
        }
      ]
    }
  ]
}</code></pre>
