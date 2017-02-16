Statsd Client
=============

[![Build status](https://ci.appveyor.com/api/projects/status/fklgn25u3k66qu3v?svg=true)](https://ci.appveyor.com/project/DarrellMozingo/statsd-csharp-client)
[![NuGet Version](http://img.shields.io/nuget/v/StatsdClient.svg?style=flat)](https://www.nuget.org/packages/StatsdClient/)

A .NET Standard compatible C# client to interface with Etsy's excellent [statsd](https://github.com/etsy/statsd) server.

Install the client via NuGet with the [StatsdClient package](http://nuget.org/packages/StatsdClient).

##Usage

At app startup, configure the `Metrics` class:

``` C#
Metrics.Configure(new MetricsConfig
{
  StatsdServerName = "hostname",
  Prefix = "myApp.prod"
});
```

Start measuring all the things!

``` C#
Metrics.Counter("stat-name");
Metrics.Time(() => myMethod(), "timer-name");
var result = Metrics.Time(() => GetResult(), "timer-name");
var result = await Metrics.Time(async () => await myAsyncMethod(), "timer-name");
Metrics.GaugeAbsoluteValue("gauge-name", 35);
Metrics.GaugeDelta("gauge-name", -5);
Metrics.Set("something-special", "3");

using (Metrics.StartTimer("stat-name"))
{
  // Lots of code here
}
```

##Advanced Features

To enable these see the `MetricsConfig` class used above.

* `UseTcpProtocol`: sends metrics to statsd via TCP. While supported, UDP is recommended in most cases. If you need TCP reliability, a relay service running locally on the server which you'd send UDP to, and it would relay via TCP, is advised.

##Contributing

See the [Contributing](CONTRIBUTING.md) guidelines.
