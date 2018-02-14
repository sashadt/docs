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

* [Online Analytics Service]() - This service provides analytic processing of event streams from various source applications in real-time. This is an Apex application, which provides the backend query service. The visualization for this query service is provided by [Apache Superset](#superset).
* [Drools Workbench]() - This service is a web application and repository which is used to manage Drools assets. It provides the capability to change the application functionality by using Drools-based rules. You can create, edit, or version the rules and apply these rules in the application.
* [Superset](#superset) - This service provides a rich set of data visualizations with an easy-to-use interface for exploring and visualizing data. Using this service, you can create and share dashboards as well as control the data sources that must be displayed on the dashboards.

# Management

You can view and manage installed services using the **Services** page. To navigate to the **Services** page, follow the steps below:

1. Click the Settings ![](images/dtservices/cog-wheel.png) icon located on the upper most right section of the DT RTS console.
2. Select the **Services** menu item from the dropdown menu.  The **Services** page is displayed with the list of installed services.

The following details can be found in the services table on the **Services** page:

| Item | Description |
| ---- | ----------- |
| name | The service name, which can be clicked to navigate to the service instance page. |
| enabled | The service status should be `RUNNING` if this field is `true` (checked).<br/>The status should be `STOPPED` if this field is `false`.<br/>The Gateway monitors all **enabled** services to make sure they are running.  |
| status | The state of the service. |
| started | The duration since the service was started. |
| uptime | Number of hours the service has been running. |
| type | The service type. Possible values are `docker` and `apex`. |
| active apps | The active Apex applications that depend on the service. |
| memory | Memory allocated by the service. |

<a name="all_service_status"></a>
Below are possible service status:

| Status | Description |
| ------ | ----------- |
| INSTALLING | The service is being installed.  This status is typically shown during service download or installation. |
| STOPPED | The service is installed, but not running. |
| STARTING | The service is installed and is starting up. |
| RUNNING | The service is installed and running. |
| STOPPING | The service is being stopped. |
| REMOVING | The service is being deleted. Once deleted, it should disappear from the table on the **Services** page. |
| FAILED | The service is installed but failed to start or ended unexpectedly. |

The following actions can be performed on this page:

* [Create new service](#create_new_service)
* [Import packaged services](#import_packaged_service)
* [View service instance](#view_service_instance)
* [Edit service](#edit_service)
* [Start services](#start_services)
* [Stop services](#stop_services)
* [Clone service](#clone_service)
* [Delete services](#delete_services)

<a name="create_new_service"></a>

#### Create New Service

To create a new service, follow the steps below:

1. Navigate to the **Services** page.
2. Click the **create new** button. The **Create Service** dialog is shown.
3. Enter the following details:

    | Item | Description |
    | ----- | ----------- |
    | Name | Enter the name of the service. This should be a unique name. |
    | Description | Enter a description about the service. |
    | Type | Select a service type.<br/>`docker` - Docker container as a service.<br/>`apex` - Apex application as a service. |
    | Source URL | Specify the location of the Docker image or the Apex application image. |
    | Docker Run<br/>_(Optional)_ | Enter the Docker command arguments to be used when the Docker service container starts.<br/>**Note**: This entry will only be shown if the service type is `docker`. |
    | Docker Exec<br/>_(Optional)_ | Execute the shell command inside the docker container after it is launched.<br/>**Note**: This entry will only be shown if the service type is `docker`. |
    | Apex App Name | Enter the application name that exists in the Apex APA image which will be launched when the service starts.<br/>**Note**: This entry will only be shown if the service type is `apex`. |
    | Apex Launch Properties<br/>_(Optional)_ | Enter Apex launch properties. Click the **Add** button to add additional properties. Enter the names and corresponding values.<br/>**Note**: This entry will only be shown if the service type is `apex`. |
    | Proxy Address<br/>_(Optional)_ | Port or host:port to which the Gateway proxy path forwards requests. |
    | Proxy Request Headers<br/>_(Optional)_ | Enter headers to be added to the request made by the Gateway to the proxy destination. Click the **Add** button to add additional headers. |
    | Proxy Response Replacements<br/>_(Optional)_ | Enter the response replacement definitions which represents the text replacement processing to be performed on the response body by the Gateway proxy. Click the **Add** button to add additional replacement definitions.|

4. Click the **Create** button to create the new service and install it.

For more details and examples regarding the items in the table above, see the [Services Property](#services_property) section below.

Sample Docker create service dialog.

![](/images/dtservices/create-service-docker.png)

Sample Apex create service dialog.

![](/images/dtservices/create-service-apex.png)

<a name="import_packaged_service"></a>

#### Import Packaged Service

Packaged services are pre-defined services included in application packages that are uploaded in the cluster.  These services can be installed as-is or with different settings.

To install a packaged service, follow the steps below:

1. Navigate to the **Services** page.
2. Click the **import** button. The **Import from Packaged Services** page is displayed with the list of available packaged services in application packages.
3. Click the **import** button of a service to be imported. An **Import Packaged Service** dialog is shown.
4. Edit the applicable entries and click the **Import** button to install the service.

<a name="view_service_instance"></a>

#### View Service Instance

1. Navigate to the **Services** page.
2. Click the service name to navigate to the service instance page.

The following sections can be found on the **Service Instance** page:

**Service Status and Actions**

This section shows the **service name**, **type**, **status**, **uptime** and **currently allocated memory** if the service is running.  It also contains the applicable actionable buttons such as **view app**, **start**, **stop**, **edit**, **copy** and **delete**.  Note that the **view app** button is only visible if the service type is `apex` and the service is running.

**Service Details**

This table shows the configuration of the service.  It also contains the Apex application ID if the service type is `apex` and the service is running.

**Proxy URL**

This section shows the proxy URL that users can use to access data provided by the service through the Gateway proxy.  The Gateway applies proxy request headers and proxy replace string settings when processing this URL requests.

**Dependent Active Apps**

This section shows the Apex applications that depend on this service.  The table will show the application ID application name, application status and the application running username.  Users can click on the application ID or name to navigate to the running Apex application instance page.

<a name="edit_service"></a>

#### Edit Service

Services are automatically installed when an associated application is launched. However, you can change the settings of the services based on your requirements and restart the services.

**Note**: Only **STOPPED** services can be edited.

To edit a service, follow the steps below:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **Edit** button. The **Edit Service** dialog is shown.
3. Edit the settings and click the **Save** button. The new settings are saved and will be applied when the service is restarted.

**Note**: You can also edit a service on the service instance page.

<a name="start_services"></a>

#### Start Services

To start a service, follow the steps below:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **Start** button.

**Note**: You can also start a service on the service instance page.

<a name="stop_services"></a>

#### Stop Services

To stop a service, follow the steps below:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **Stop** button. A **Stop Service** modal is shown.
3. Click the **Stop** button to stop the service.

**Note**: You can also stop a service on the service instance page.

<a name="clone_service"></a>

#### Clone Service

You can clone, edit, and save a service configuration as a new service.

To clone a service, follow the steps below:

1. Navigate to the **Services** page.
2. Select a service to clone and click the **copy** button.  The **Create Service** dialog is shown with the selected service configurations pre-filled.
3. Change the service name and applicable settings.<br/>Service name must be different from the original service name because it must be unique.
4. Click the **Create** button to create the new service.<br/>If the original service is enabled, then the new service will be installed and started.<br/>If the original service isn't enabled, then the new service will be installed, but not started.

**Note**: You can also clone a service on the service instance page.

<a name="delete_services"></a>

#### Delete Services

Services can be deleted for an application from the Services management page.

To stop or start the services, follow the steps below:

1. Navigate to the **Services** page.
2. Select a service from the services list and click the **delete** button.  The delete service confirmation modal is shown.
3. Click the **Delete** button to confirm that you want to delete the service.

**Note**: You can also delete a service on the service instance page.

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

Services and dependent applications can be defined and included in the application package.  This service descriptor is defined in the **services.json** file.  This file is located in the **/src/main/resources/resources** directory of your Apex project.  When the project is built and packaged as an APA file, the **services.json** file is placed in the **/resources** directory inside the APA file.

The **services.json** file contains two root level properties:

* [Services Property](#services_property)
* [Applications Property](#applications_property)

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
| srcURL | string | Specify the name of the Docker image if the service is Docker based or specify the path of the Apex application package if the service is Apex based.<br/><br/>An example of a Docker srcURL: `datatorrent/superset-fpa:1.4.0`<br/><br/>An example of an Apex srcURL:<br/>`${.dt.gateway.artifactHubLocation}/ws/v1/artifacts/com.datatorrent/`<br/>`dt-apoxi-oas/1.4.0-SNAPSHOT/download`<br/><br/>Another example of an Apex URL: `file:///path/to/apppackage.apa` |
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
| followRedirect<br/>_(Optional, default: true)_ | boolean | If this property is true, then the Gateway proxy will perform redirect when it sees the HTTP status code 302 in the HTTP response header from the service.  Therefore, the browser surfing the service proxy URL will never encounter the hTTP status code 302.<br/>**Warning**: Omitting this property or setting it to true may cause a maximum redirect error in the Gateway proxy. |
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
