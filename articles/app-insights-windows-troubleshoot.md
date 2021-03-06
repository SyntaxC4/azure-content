<properties 
	pageTitle="Troubleshoot Application Insights in a Windows devices" 
	description="Troubleshooting guide and question and answer." 
	services="application-insights" 
    documentationCenter=""
	authors="alancameronwills" 
	manager="keboyd"/>

<tags 
	ms.service="application-insights" 
	ms.workload="tbd" 
	ms.tgt_pltfrm="ibiza" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="03/27/2015" 
	ms.author="awills"/>
 
# Troubleshooting and Q&A for Application Insights for Windows devices

Questions or problems with [Visual Studio Application Insights in Windows][windows]? Here are some tips.



## No data 

*I added Application Insights successfully and ran my app, but I've never seen data in the portal.*

* Wait a minute and click Refresh. Currently, refresh isn't automatic.
* Check that you have an instrumentation key defined in the ApplicationInsights.config file, and that it is the same as the key in the Application Insights portal. To see the key, click Essentials on the overview blade.
* Make sure your app [requests outgoing network access](https://msdn.microsoft.com/library/windows/apps/hh452752.aspx).
* Is there a firewall between your emulator or test device and the Application Insights portal? You might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.
* In the Microsoft Azure start board, look at the service status map. If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.

#### I used to see data, but it has stopped

* Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/)


## How do I add Application Insights to a Universal App?

Add the NuGet packages manually to each device project in your solution. See [Getting Started - Universal apps][universal].

## Disabling telemetry

*How can I disable telemetry collection?*

In code:

    TelemetryConfiguration config = TelemetryConfiguration.Active;
    config.TrackingIsDisabled = true;

## Changing the target resource

*How can I change which Application Insights resource my project sends data to?*

In the new Application Insights overview blade, open Essentials and copy the instrumentation key.

Paste the key into your ApplicationInsights.config file in the `<InstrumentationKey>` node.

Or, if you want to change targets at run time, use:

     var telemetry = new TelemetryClient();
     telemetry.Context.InstrumentationKey = newKey;
    
## How do I monitor a client-server app?

There are two ways of doing this:

* Create two Application Insights resources (with different instrumentation keys), for the client and the server. But create them in the same Azure resource group. That makes it easy to switch between one and the other.
* Use one Application Insights resource and put its instrumentation key into both client and server projects. Then you can correlate metrics and events from the two sources.

To help correlate events in the client and server, generate an operation id for each request. Transmit it between the client and server, add it to the telemetry at both ends:

    telemetry.Context.OperationId = opid;


## The Azure start screen

*I'm looking at [the Azure portal](http://portal.azure.com). Does the map tell me something about my app?*

No, it shows the health of Azure servers around the world.

*From the Azure start board (home screen), how do I find data about my app?*

Assuming you [already set up your app for Application Insights][windows], click Browse, select Application Insights, and select the resource you created for your app. To get there faster in future, you can pin the resource to the start board.

## Data retention 

*How long is data retained in the portal? Is it secure?*

See [Data retention and privacy][data].

## Next steps

*I set up Application Insights for my Java server app. What else can I do?*

* [Monitor availability of your web pages][availability]
* [Monitor web page usage][usage]
* [Track usage and diagnose issues in your device apps][platforms]
* [Write code to track usage of your app][track]
* [Capture diagnostic logs][javalogs]


## Get help

* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[alerts]: app-insightss-alerts.md
[android]: https://github.com/Microsoft/AppInsights-Android
[api]: app-insights-custom-events-metrics-api.md
[apiproperties]: app-insights-custom-events-metrics-api.md#properties
[apiref]: http://msdn.microsoft.com/library/azure/dn887942.aspx
[availability]: app-insights-monitor-web-app-availability.md
[azure]: insights-perf-analytics.md
[azure-availability]: insights-create-web-tests.md
[azure-usage]: insights-usage-analytics.md
[azurediagnostic]: insights-how-to-use-diagnostics.md
[client]: app-insights-web-track-usage.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[data]: app-insights-data-retention-privacy.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[exceptions]: app-insights-web-failures-exceptions.md
[export]: app-insights-export-telemetry.md
[exportcode]: app-insights-code-sample-export-telemetry-sql-database.md
[greenbrown]: app-insights-start-monitoring-app-health-usage.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[javareqs]: app-insights-java-track-http-requests.md
[knowUsers]: app-insights-overview-usage.md
[metrics]: app-insights-metrics-explorer.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[older]: http://www.visualstudio.com/get-started/get-usage-data-vs
[perf]: app-insights-web-monitor-performance.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[roles]: app-insights-role-based-access-control.md
[start]: app-insights-get-started.md
[trace]: app-insights-search-diagnostic-logs.md
[track]: app-insights-custom-events-metrics-api.md
[usage]: app-insights-web-track-usage.md
[windows]: app-insights-windows-get-started.md
[universal]: app-insights-windows-get-started.md#universal
[windowsCrash]: app-insights-windows-crashes.md
[windowsUsage]: app-insights-windows-usage.md

