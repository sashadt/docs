Running Demo Applications
=================================

DataTorrent RTS includes a number of demo applications and they are available for import from the **AppFactory** section of the DataTorrent management console.

Importing Demo Applications
--------------------------------------------------------------------------------

1.  Navigate to **AppFactory** section of the DataTorrent console.
2.  Select one of the available packages, such as *Pi Demo* and click *Import* button.
3.  Imported application packages and included applications will be listed under **Develop > Application Packages** page.

Launching Demo Applications
--------------------------------------------------------------------------------

Once imported, applications can be launched with a single click.  *Note*: Ensure Hadoop YARN and HDFS services are active and ready by checking for errors in the DataTorrent console before launching demo applications.

1.  Navigate to **Develop > Application Packages**, and select one of the imported demo packages.  In this example we will use **PiDemo** application package.

2.  From the list of available Applications, locate PiDemo and click the launch button.

    ![](images/sandbox/pidemo-list.png)

3.  Proceed with default options on launch confirmation screen by clicking the Launch button.

4.  Once launched, view the running application by following the link provided in the launch confirmation dialog, or by navigating to the **Monitor** section of the console and selecting the launched application.

    ![](images/sandbox/pidemo-success.png)

More information about using DataTorrent console is available in [dtManage Guide](dtmanage.md)



Configuring Launch Parameters
--------------------------------------------------------------------------------

Some applications may require additional configuration changes prior to launching.  Configuration changes can be made on the launch confirmation screen or manually applied to `~/.dt/dt-site.xml` configuration file.  These typically include adding Twitter API keys for twitter demo, or changing performance settings for larger applications.

1.  Navigate to **AppFactory** of the DataTorrent console.  In this example, we will use **Twitter Demo** application package. Click *Import* button. 

2.  Navigate to **Develop > Application Packages**. From the list of Applications, select TwitterDemo and press the corresponding launch button.

3.  Retrieve Twitter API access information by registering for <a href="https://dev.twitter.com/" target="\_blank">Twitter Developer</a> account, creating a new <a href="https://apps.twitter.com/app/new" target="\_blank">Twitter Application</a>, and navigating to Keys and Access Tokens tab.  Twitter Demo application requires the following to be specified by the user:

    dt.operator.TweetSampler.accessToken
    dt.operator.TweetSampler.accessTokenSecret
    dt.operator.TweetSampler.consumerKey
    dt.operator.TweetSampler.consumerSecret

4.  Select *Specify custom properties* on the launch confirmation screen, click *add required properties* button, and provide Twitter API access values.  Choose to save this configuration as `twitter.xml` file and proceed to Launch the application.

    ![](images/sandbox/twitterdemo-launch.png)

5.  Once launched, view the running application by following the link provided in the launch confirmation dialog, or by navigating to the **Monitor** section of the console and selecting the launched application.

6.  View the top 10 tweeted hashtags in real time by generating and viewing the [dashboard](dtdashboard.md).

Stopping Applications
--------------------------------------------------------------------------------

Applications can be shut down or killed from the Monitor section of [dtManage](dtmanage.md) by selecting application from the list and clicking `shutdown` or `kill` buttons.
