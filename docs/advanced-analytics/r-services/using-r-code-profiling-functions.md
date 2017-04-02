---
title: "使用分析函数的 R 代码 | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# 使用分析函数的 R 代码
除了使用 SQL Server 资源和工具监视 R 脚本执行，你可以使用提供的其他 R 包的性能工具以获取有关内部函数调用的详细信息。 本主题提供一些基本的资源，可帮助你入门的列表。 对于专家指导，我们建议章上 [性能](http://adv-r.had.co.nz/Performance.html) 簿""高级 R""，通过 Hadley Wickham 中。

## <a name="using-rprof"></a>使用 RPROF

*rprof* 是基程序包中包含一个函数 **utils**, ，默认情况下它将被加载。 一个优点 *rprof* 是其执行采样，因此减少了从监视的性能负载。

若要使用在你的代码中进行分析的 R，则调用此函数，并指定其参数，包括将写入日志文件的位置的名称。 请参阅有关的帮助 *rprof* 有关详细信息。

一般情况下， *rprof* 通过写出到文件中，指定时间间隔的调用堆栈函数工作原理。 然后，可以使用 *summaryRprof* 函数来处理输出文件。 

分析可以打开和关闭在代码中。 若要启用分析，挂起分析，然后再重新启动它，你将使用的一系列调用到 *rprof*:

1. 指定分析的输出文件。

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. 关闭分析
    ```R
    Rprof(NULL)
    ```
    
3. 重新启动分析
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE] 使用此功能要求在运行代码的计算机上安装 Windows Perl。 因此，我们建议您在 R 环境中，开发过程中分析代码，然后将调试的代码部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系统函数

R 语言包括许多基本包函数用于返回系统变量的内容。 

例如，作为 R 代码的一部分，你可以使用 `Sys.timezone` 若要获取当前时区，或 `Sys.Time` 来获取系统时间从。 

若要获取有关各个 R 系统函数的信息，请键入函数名称作为 R 的参数 `help()` 从 R 命令提示符的函数。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>调试和在 R 中进行分析

Microsoft R Open，默认情况下安装的文档包括手动开发讨论分析和调试详细信息中的 R 语言扩展。

联机还有章︰ [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 帮助文件的位置

C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\doc\manual


