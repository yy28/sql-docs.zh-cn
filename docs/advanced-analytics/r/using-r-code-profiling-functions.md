---
title: "使用 R 代码分析函数 | Microsoft Docs"
ms.custom: 
ms.date: 11/29/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: "6"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88d8e1c0948a51ab8ed6aaeb5a74e771bba95032
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="using-r-code-profiling-functions"></a>使用 R 代码分析函数
除了使用 SQL Server 资源和工具来监视 R 脚本执行外，还可以使用由其他 R 包提供的性能工具来获取有关内部函数调用的详细信息。 本主题提供了引导你入门的一些基本资源的列表。 若要查看专家指导，建议你参阅由 Hadley Wickham 编写的“Advanced R”一书中有关[性能](http://adv-r.had.co.nz/Performance.html)的一章。

## <a name="using-rprof"></a>使用 RPROF

*rprof* 是默认加载的基础包 **utils** 中的一个函数。 *rprof* 的一个优点是它会执行采样，从而降低监视对性能造成的影响。

要在代码中使用 R 分析，请调用此函数并指定其参数，包括将写入的日志文件的位置名称。 有关详细信息，请参阅 *rprof* 的帮助。

通常，*rprof* 函数会以指定的间隔将调用堆栈写入到一个文件中。 然后，你可以使用 *summaryRprof* 函数来处理输出文件。 

可以在你的代码中打开或关闭分析。 要打开分析，请暂停分析，然后重新启动它，你将使用对 *rprof* 的调用序列：

1. 指定分析输出文件。

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


> [!NOTE]
> 若要使用此函数，需要在运行代码的计算机上安装 Windows Perl。 因此，建议你在开发过程中在 R 环境中分析代码，然后将调试后的代码部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系统函数

R 语言包括了许多用于返回系统函数的内容的基础包。 

例如，你可以在 R 代码中使用 `Sys.timezone` 来获取当前时区，或者使用 `Sys.Time` 来从 R 获取系统时间。 

若要获取有关各个 R 系统函数的信息，请在 R 命令提示符下键入函数名称作为 R `help()` 函数的参数。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>在 R 中进行调试和分析

默认情况下安装的 Microsoft R Open 的文档包括了一个有关为 R 语言开发扩展的手册，其中详细讨论了分析和调试。

还提供了该章的在线版本：[https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 帮助文件的位置

C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual



