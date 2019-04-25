---
title: 使用 R 代码分析函数-SQL Server 机器学习服务
description: 提高性能并获取有关 SQL Server 上的 R 计算更快的结果，通过使用 R 分析函数来返回有关内部函数调用的信息。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c9195a6c2b9a2192e9d8fd04ce3e5d2592b1b23e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642258"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>使用 R 代码分析函数来提高性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

除了使用 SQL Server 资源和工具来监视 R 脚本执行外，还可以使用由其他 R 包提供的性能工具来获取有关内部函数调用的详细信息。 

> [!TIP]
> 本文提供了基本的资源来帮助你入门。 专家指导，我们建议*性能*主题中[由 Hadley wickham 编写的"Advanced R"](http://adv-r.had.co.nz)。

## <a name="using-rprof"></a>使用 RPROF

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof)取决于基础包中包含[ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)，默认情况下它将被加载。 

通常，*rprof* 函数会以指定的间隔将调用堆栈写入到一个文件中。 然后，可以使用[ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof)函数来处理输出文件。 *rprof* 的一个优点是它会执行采样，从而降低监视对性能造成的影响。

要在代码中使用 R 分析，请调用此函数并指定其参数，包括将写入的日志文件的位置名称。 可以在你的代码中打开或关闭分析。 下面的语法演示了基本用法： 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> 若要使用此函数，需要在运行代码的计算机上安装 Windows Perl。 因此，建议你在开发过程中在 R 环境中分析代码，然后将调试后的代码部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系统函数

R 语言包括了许多用于返回系统函数的内容的基础包。 例如，你可以在 R 代码中使用 `Sys.timezone` 来获取当前时区，或者使用 `Sys.Time` 来从 R 获取系统时间。 

若要获取有关各个 R 系统函数的信息，请在 R 命令提示符下键入函数名称作为 R `help()` 函数的参数。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>在 R 中进行调试和分析

Microsoft R Open，默认情况下安装的文档包括开发的讨论了 R 语言扩展的手册[分析和调试](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)在详细信息。 您可以在 C:\Program Files\Microsoft SQL Server\MSSQL13 向计算机上发现相同的文档。MSSQLSERVER\R_SERVICES\doc\manual。

## <a name="see-also"></a>另请参阅

+ [utils R 包](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["高级的 R"由 Hadley wickham 编写](http://adv-r.had.co.nz)
