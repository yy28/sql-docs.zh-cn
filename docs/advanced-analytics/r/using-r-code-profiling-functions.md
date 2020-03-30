---
title: 使用 R 代码分析函数
description: 通过使用 R 分析函数返回有关内部函数调用的信息，提高性能并在 SQL Server 上更快获得 R 计算结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e03ae1a8c4cdab87f46f63da6271886b4518b5e3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68715012"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>使用 R 代码分析函数提高性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

除了使用 SQL Server 资源和工具来监视 R 脚本执行外，还可以使用由其他 R 包提供的性能工具来获取有关内部函数调用的详细信息。 

> [!TIP]
> 本文提供入门的基本资源。 要查看专家指导，建议参阅[由 Hadley Wickham 编写的《Advanced R》](http://adv-r.had.co.nz)中的“性能”部分  。

## <a name="using-rprof"></a>使用 RPROF

[rprof](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) 是默认加载的基础包 [utils](https://www.rdocumentation.org/packages/utils/versions/3.5.1) 中的一个函数   。 

通常，*rprof* 函数会以指定的间隔将调用堆栈写入到一个文件中。 然后，可以使用 [summaryRprof](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 函数来处理输出文件  。 *rprof* 的一个优点是它会执行采样，从而降低监视对性能造成的影响。

要在代码中使用 R 分析，请调用此函数并指定其参数，包括将写入的日志文件的位置名称。 可以在你的代码中打开或关闭分析。 以下语法说明了基本用法： 

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

默认情况下安装的 Microsoft R Open 的文档包括了一个有关为 R 语言开发扩展的手册，其中详细讨论了[分析和调试](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)。 可以在计算机的 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manua 位置找到相同的文档。

## <a name="see-also"></a>另请参阅

+ [utils R 包](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ [由 Hadley Wickham 编写的《Advanced R》](http://adv-r.had.co.nz)
