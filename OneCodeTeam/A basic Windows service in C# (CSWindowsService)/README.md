# A basic Windows service in C# (CSWindowsService)
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- Windows SDK
## Topics
- Windows Service
## Updated
- 03/01/2012
## Description

<h1>WINDOWS SERVICE (CSWindowsService)</h1>
<h2>Introduction</h2>
<p class="MsoNormal">This code sample demonstrates creating a very basic Windows Service application in Visual C#. The example Windows Service logs the service start and stop information to the Application event log, and shows how to run the main function
 of the service in a thread pool worker thread. You can easily extend the Windows Service skeleton to meet your own business requirement.<span style="">&nbsp;
</span></p>
<h2>Running the Sample</h2>
<p class="MsoNormal"><span style="">The following steps walk through a demonstration of the Windows Service sample.
</span></p>
<p class="MsoNormal"><span style="">Step1. After you successfully build the sample project in Visual Studio 2010, you will get a service application: CSWindowsService.exe.
</span></p>
<p class="MsoNormal"><span style=""><img src="52989-image.png" alt="" width="576" height="159" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">Step2. Run Visual Studio 2010 Command Prompt as administrator, navigate to the output folder of the sample project, and enter the following command to install the service.
</span></p>
<p class="MsoNormal"><span style="background:#D9D9D9"><span style="">&nbsp; </span>
InstallUtil.exe CSWindowsService.exe </span></p>
<p class="MsoNormal"><span style="">The service is successfully installed if the process outputs:
</span></p>
<p class="MsoNormal"><span style=""><img src="52990-image.png" alt="" width="576" height="689" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">If you do not see this output, please look for the CSWindowsService.InstallLog file in the ouput folder, and investigate the cause of failure.
</span></p>
<p class="MsoNormal"><span style="">Step3. Open Service Management Console (services.msc). You should be able to find &quot;CSWindowsService Sample Service&quot; in the service list.
</span></p>
<p class="MsoNormal"><span style=""><img src="52991-image.png" alt="" width="576" height="279" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">Step4. Right-click the CSWindowsService service in Service Management Console and select Start to start the service. Open Event Viewer, and navigate to Windows Logs / Application. You should be able to see two events from
 CSWindowsService with event messages: &quot;CSWindowsService in OnStart.&quot; and &quot;Service started successfully.&quot;
</span></p>
<p class="MsoNormal"><span style=""><img src="52992-image.png" alt="" width="576" height="279" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">Right-click the service in Service Management Console and select Stop to stop the service. You will see two new events from CSWindowsService in Event Viewer / Windows Logs / Application with messages: &quot;CSWindowsService
 in OnStop&quot; and &quot;Service stopped successfully&quot;. </span></p>
<p class="MsoNormal"><span style=""><img src="52993-image.png" alt="" width="576" height="308" align="middle">
</span><span style=""></span></p>
<p class="MsoNormal"><span style="">Step5. To uninstall the service, enter the following command in Visual Studio 2010 Command Prompt running as administrator.
</span></p>
<p class="MsoNormal"><span style="background:#D9D9D9"><span style="">&nbsp; </span>
InstallUtil /u CSWindowsService.exe </span></p>
<p class="MsoNormal"><span style="">If the service is successfully stopped and removed, you would see this output:
</span></p>
<h2><span style=""><img src="52994-image.png" alt="" width="576" height="689" align="middle">
</span><span style="">&nbsp;</span><span style=""> </span></h2>
<h2><span style="">Setup and Removal </span></h2>
<h3><span style="">In the Development Environment </span></h3>
<p class="MsoNormal"><b style=""><span style="">A. Setup </span></b></p>
<p class="MsoNormal"><span style="">Run the command &quot;Installutil.exe CSWindowsService.exe&quot; in an elevated Visual Studio 2010 Command Prompt. It installs CSWindowsService.exe as a service to the local service control manager database.
</span></p>
<p class="MsoNormal"><b style=""><span style="">B. Cleanup </span></b></p>
<p class="MsoNormal"><span style="">Run the command &quot;Installutil.exe /u CSWindowsService.exe&quot; in an elevated Visual Studio 2010 Command Prompt. It stops and removes the CSWindowsServiceservice from the local service control manager database.
</span></p>
<h3><span style="">In the Deployment Environment </span></h3>
<p class="MsoNormal"><b style=""><span style="">A. Setup </span></b></p>
<p class="MsoNormal"><span style="">Install <span class="SpellE">CSWindowsServiceSetup</span>(x86).<span class="SpellE">msi</span>, the output of the CSWindowsServiceSetup(x86) setup project, on
<span class="GramE">a</span> x86 operating system. If the target platform is x64, install CSWindowsServiceSetup(x64).msi outputted by the CSWindowsServiceSetup(x64) setup project.
</span></p>
<p class="MsoNormal"><b style=""><span style="">B. Removal </span></b></p>
<p class="MsoNormal"><span style="">Uninstall CSWindowsServiceSetup(x86).msi, the output of the CSWindowsServiceSetup(x86) setup project, on
<span class="GramE">a</span> x86 operating system. If the target platform is x64, uninstall SWindowsServiceSetup(x64).msi outputted by the CSWindowsServiceSetup(x64) setup project.
</span></p>
<h2>Using the Code</h2>
<h3>A. Creating Windows Service<span style=""> </span></h3>
<p class="MsoNormal"><span style=""><a href="http://msdn.microsoft.com/en-us/library/aa983583.aspx">http://msdn.microsoft.com/en-us/library/aa983583.aspx</a>
</span></p>
<p class="MsoNormal">Step1. In Visual Studio 2010, add a new Visual C# / Windows / Windows Service project named CSWindowsService. The project template automatically adds a component class named Service1 that inherits from System.ServiceProcess.ServiceBase.
</p>
<p class="MsoNormal">Step2. Rename the default Service1 to the name &quot;SampleService&quot;. Open the service in designer and set the ServiceName property to be CSWindowsService.
</p>
<p class="MsoNormal">Step3. To add custom event log functionality to your service, drag and drop an event log component from toolbox to the design view, and set its Log property to be Application, and its Source to be CSWindowsService. The event log component
 will be used to log some messages to the Application log. </p>
<p class="MsoNormal">Step4. To define what occurs when the service starts and stops, in the Code Editor, locate the OnStart and OnStop methods that were automatically overridden when you created the project, and write code to determine what occurs when the
 service starts running. In this example, we log the service start and stop information to the Application log, and show how to run the main function of the service in a thread pool worker thread.<span style="">
</span>SampleService.OnStart, which is executed when the service starts, calls EventLog.WriteEntry to log the service-start information. And it calls ThreadPool.QueueUserWorkItem to queue the main service function (SampleService.ServiceWorkerThread) for execution
 in a worker thread. </p>
<p class="MsoNormal"><b style="">NOTE</b>: A service application is designed to be long running. Therefore, it usually polls or monitors something in the system. The monitoring is set up in the OnStart method. However, OnStart does not actually do the monitoring.
 The OnStart method must return to the operating system after the service's operation has begun. It must not loop forever or block. To set up a simple<span style="">
</span>monitoring mechanism, one general solution is to create a timer in OnStart. The timer would then raise events in your code periodically, at which time your service could do its monitoring. The other solution is to spawn a new
</p>
<p class="MsoNormal">thread to perform the main service functions, which is demonstrated in this code sample.
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected override void OnStart(string[] args)
{
    // Log a service start message to the Application log.
    this.eventLog1.WriteEntry(&quot;CSWindowsService in OnStart.&quot;);


    // Queue the main service function for execution in a worker thread.
    ThreadPool.QueueUserWorkItem(new WaitCallback(ServiceWorkerThread));
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">SampleService.OnStop, which is executed when the service stops, calls EventLog.WriteEntry to log the service-stop information. Next, it sets the member varaible 'stopping' as true to indicate that the service is stopping and waits for
 the finish of the main service function that is signaled by the 'stoppedEvent' event object.
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected override void OnStop()
{
    // Log a service stop message to the Application log.
    this.eventLog1.WriteEntry(&quot;CSWindowsService in OnStop.&quot;);


    // Indicate that the service is stopping and wait for the finish 
    // of the main service function (ServiceWorkerThread).
    this.stopping = true;
    this.stoppedEvent.WaitOne();
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">SampleService.ServiceWorkerThread runs in a thread pool worker thread. It performs the main function of the service such as the communication with client applications through a named pipe. In order that the main function finishes gracefully
 when the service is about to stop, it should periodically check the 'stopping' varaible. When the function detects that the service is stopping, it cleans up the work and signal the 'stoppedEvent' event object.
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
private void ServiceWorkerThread(object state)
{
    // Periodically check if the service is stopping.
    while (!this.stopping)
    {
        // Perform main service function here...


        Thread.Sleep(2000);  // Simulate some lengthy operations.
    }


    // Signal the stopped event.
    this.stoppedEvent.Set();
}

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<h3>B. Adding Installer to the service</h3>
<p class="MsoNormal"><span style=""><a href="http://msdn.microsoft.com/en-us/library/aa984263.aspx">http://msdn.microsoft.com/en-us/library/aa984263.aspx</a>
</span></p>
<p class="MsoNormal">Step1. Open SampleService.cs in Designer, and click the background of the designer to select the service itself, instead of any of its contents.
<span class="GramE">With the designer in focus, right-click, and then click Add Installer.</span> By default, a component class that contains two installers is added to your project. The component is named ProjectInstaller, and the installers it contains
 are the installer for your service and the installer for the service's associated process.
</p>
<p class="MsoNormal">Step2. In Design view for ProjectInstaller, click serviceInstaller1. In the Properties window, set the ServiceName property to CSWindowsService. Set the
<span class="SpellE">DisplayName</span> property to <span class="SpellE">CSWindowsService</span> Sample Service. In the designer, click serviceProcessInstaller1. Set the Account property to LocalService. This will cause the service to be installed and to
 run on a local service account. </p>
<p class="MsoNormal"><b style="">Security Note</b>: In this code sample, the service is configured to run as
<span class="SpellE">LocalService</span>, instead of <span class="SpellE">LocalSystem</span>. The LocalSystem account has broad permissions. Use the LocalSystem account with caution, because it might increase your risk of attacks from malicious software.
 For tasks that do not need broad permissions, consider using the LocalService account, which acts as a non-privileged user on the local computer and presents anonymous credentials to any remote server.
</p>
<h3>C. Creating a setup project for the service to facilitate the deployment </h3>
<p class="MsoNormal">Step1. Add a new Other Project Types / Setup and Deployment Projects / Setup Project named
<span class="SpellE">CSWindowsServiceSetup</span>. </p>
<p class="MsoNormal">Step2. To add CSWindowsService.exe to the setup project, right-click
<span class="SpellE">CSWindowsServiceSetup</span>, point to Add, and then click Project Output. Select
<span class="SpellE">CSWindowsService</span> in the Project box and choose Primary Output from the list. A project item for the primary output of CSWindowsService is added to the setup project.
</p>
<p class="MsoNormal">Step3. By default, the target platform of the setup project is x86. If you want to build a setup that targets the x64 platform, click the setup project, and choose &quot;x64&quot; as the TargetPlatform in the Properties dialog.
</p>
<p class="MsoNormal">Step4. Now add a custom action to install the CSWindowsService.exe file. Right-click the setup project in Solution Explorer, point to View, and then
<span class="GramE">click</span> Custom Actions. In the Custom Actions editor, right-click the Custom Actions node and click Add Custom Action. Double-click the Application Folder in the list to open it, select Primary Output from
<span class="SpellE">CSWindowsService</span> (Active), and click OK. The primary output is added to all four nodes of the custom actions �� Install, Commit, Rollback, and Uninstall. In Solution Explorer, right-click the
<span class="SpellE">CSWindowsServiceSetup</span> project and click Build.<span style="">
</span></p>
<h2>More Information</h2>
<p class="MsoListParagraph" style=""><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/y817hyb6.aspx">MSDN: Windows Service Applications</a>
</p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
