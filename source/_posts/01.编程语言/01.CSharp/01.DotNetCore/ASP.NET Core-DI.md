---
title: 依赖注入
comments: true
tags: ASP.NET Core
date: 2018-10-22 22:48:07
---

## 1.介绍

ASP.NET Core 支持依赖关系注入 (DI) 软件设计模式，这是一种在类及其依赖关系之间实现控制反转 (IoC) 的技术。

<!--more-->

## 2.概述

依赖项是指一个对象所需的其他任何对象。

### 2.1 直接 new 的缺点

- 若使用不同的实现替换，必须修改类，违背了开闭原则；
- 层级依赖的时候，每层单独管理依赖。且依赖过多时，相关配置代码分散，不利于维护；
- 难于单元测试。

### 2.2 使用 DI 的优点

- 使用接口抽象化依赖关系实现；
- 服务容器统一管理依赖关系；
- 服务注入到类的构造函数，框架负责创建依赖关系的实例，且维护生命周期。

## 3.框架提供的服务

服务类型|生存期
----|:--:
Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory|暂时
Microsoft.AspNetCore.Hosting.IApplicationLifetime|单例
Microsoft.AspNetCore.Hosting.IHostingEnvironment|单例
Microsoft.AspNetCore.Hosting.IStartup|单例
Microsoft.AspNetCore.Hosting.IStartupFilter|暂时
Microsoft.AspNetCore.Hosting.Server.IServer|单例
Microsoft.AspNetCore.Http.IHttpContextFactory|暂时
Microsoft.Extensions.Logging.ILogger<T>|单例
Microsoft.Extensions.Logging.ILoggerFactory|单例
Microsoft.Extensions.ObjectPool.ObjectPoolProvider|单例
Microsoft.Extensions.Options.IConfigureOptions<T>|暂时
Microsoft.Extensions.Options.IOptions<T>|单例
System.Diagnostics.DiagnosticSource|单例
System.Diagnostics.DiagnosticListener|单例

## 4.服务生命周期

- Transient（暂时）：每次请求该服务时创建（Transient lifetime services are created each time they're requested），适用于轻量级、无状态的服务；
- Scoped（作用域）：每次请求创建（Scoped lifetime services are created once per request）；
  - DbContext
**警告**：在中间件内使用有作用域的服务时，请将该服务注入至 Invoke 或 InvokeAsync 方法。 请不要通过构造函数注入进行注入，因为它会强制服务的行为与单一实例类似。
- Singleton（单例）：第一次请求（或在运行 ConfigureServices 且使用服务注册指定实例）时创建，后续请求都使用相同的实例。
**警告**：从单一实例解析有作用域的服务很危险。 当处理后续请求时，它可能会导致服务处于不正确的状态。

## 5.设计服务最佳做法

- 使用依赖注入来获取依赖关系；
- 避免有状态的静态方法调用（[静态粘附](https://deviq.com/static-cling/)）；
- 避免在服务中直接实例化依赖类；
- [SOLID](https://deviq.com/solid/)
- [关注点分离](https://docs.microsoft.com/zh-cn/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns)

## 6.服务处理

容器会自动为实现 IDisposable 的类型调用 Dispose 方法，若通过实例添加到容器，则不会自动处理。

## 7.默认服务容器替换

建议使用内置容器，除非需要不支持的功能，具体如下：

- 属性注入；
- 基于名称的注入；
- 子容器；
- 自定义生命周期管理；
- 延迟初始化 Func<T>。

### 7.1 Autofac

i 安装 nuget 包：`Autofac`,`Autofac.Extensions.DependencyInjection`；
ii 配置容器，并返回 `IServiceProvider`。要使用第三方容器，Startup.ConfigureServices 必须返回 `IServiceProvider`；
```C#
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // Add other framework services

    // Add Autofac
    var containerBuilder = new ContainerBuilder();
    containerBuilder.RegisterModule<DefaultModule>();
    containerBuilder.Populate(services);
    var container = containerBuilder.Build();
    return new AutofacServiceProvider(container);
}
```
iii 在 DefaultModule 配置 Autofac
```C#
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

## 8.建议

- 避免在服务容器中直接存储数据和配置，配置应选用 `Options Pattern`；
- 避免静态访问服务（例如 IApplicationBuilder.ApplicationServices）；
- 避免使用服务定位器模式（例如 IServiceProvider.GetService）；
- 避免静态访问 `HttpContext`（例如 IHttpContextAccessor.HttpContext）。

`PS`：依赖注入是静态/全局对象访问模式的替代方法，若混合使用，则无法实现其优点。

## 参考文章

1 [依赖注入](https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1)
2 [控制反转及依赖注入模式-Martin fowler](https://www.martinfowler.com/articles/injection.html)
2 [Autofac文档](https://docs.autofac.org/en/latest/integration/aspnetcore.html)