
[![Build status Development](https://toolfactory.visualstudio.com/Core/_apis/build/status/Mectrics%20Libraries/Bluekiri.Diagnostics.Prometheus-development-CI)](https://toolfactory.visualstudio.com/Core/_build/latest?definitionId=0)
[![Build status Master](https://toolfactory.visualstudio.com/Core/_apis/build/status/Mectrics%20Libraries/Bluekiri.Diagnostics.Prometheus-CI)](https://toolfactory.visualstudio.com/Core/_build/latest?definitionId=772)

# bluekiri-diagnostics-prometheus
This library is meant to expose DiagnosticSource events as Prometheus metrics using [prometheus-net](https://github.com/prometheus-net/prometheus-net).
Currently, we exponse events from the following sources

 - HttpHandlerDiagnosticListener. This source logs the events of outgoing HTTP connections made with HttpClient.
 - Microsoft.AspNetCore. This source logs events coming from de ASP.NET Core pipeline.

## Getting started

 1. The first step is installing the following NuGet package
    ```
    Install-Package Bluekiri.Diagnostics.Prometheus
    ```
    
 2. In the application entrypoint, preferably in the main method, configure the DiagnosticListeners in the following way:
     ```csharp
     public static void Main(string[] args)
     {
        // Creating the kestrel metrics server listening
        // into another port
        var metricsServer = new KestrelMetricServer(9303);
        metricsServer.Start();

        // Subscribe the diagnostic listeners that will
        // export Prometheus metrics		
        DiagnosticListener.AllListeners.SubscribeDiagnosticListener();

        CreateWebHostBuilder(args).Build().Run();
     }
    ```
 3. Prometheus metrics will be exposed in the /metrics endpoint in the port 9303 of your host, since in this sample we configured a KestrelMetricServer in this port.

## References
- [DiagnosticSource User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)
- [HttpDiagnostics Guide](https://github.com/dotnet/corefx/blob/master/src/System.Net.Http/src/HttpDiagnosticsGuide.md)

## Contributing
Your help is always welcome. You can contribute to this project opening issues reporting bugs or new feature requests, or by sending pull requests to our development branch for new features, or to our master branch for bug fixes.
