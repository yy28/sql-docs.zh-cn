---
title: "性能案例研究 (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0f52e3200989d62e142dc2b8b287e1b1510e65df
ms.lasthandoff: 04/11/2017

---
# <a name="performance-case-study-r-services"></a>性能案例研究 (R Services)

为了演示前面部分中所述指导的效果，我们使用航班数据集中的表运行了测试。 

## <a name="tests-and-example-data"></a>测试和示例数据

共有 6 个表，每个表中包含 1000 万行：

| 表名 | Description |
| ---------- | ----------- |
| _airline_ | 使用 `rxDataStep` 从原始 xdf 文件转换的数据 |
| _airlineWithIntCol_ | *DayOfWeek* 已转换为整数而不是字符串。 另外，添加了 *rowNum* 列。 |
| _airlineWithIndex_ | 数据与 *airlineWithIntCol* 表相同，但使用 *rowNum* 列添加了单个聚集索引。 |
| _airlineWithPageComp_ | 数据与 *airlineWithIndex* 表相同，但已启用页压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| _airlineWithRowComp_ | 数据与 *airlineWithIndex* 表相同，但已启用行压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 
| _airlineColumnar_ | 包含单个聚集索引的纵栏表存储。 此表中填充了来自已清理的 csv 文件中的数据。 |

[https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) 上提供了用于执行本部分中所述测试的脚本，以及用于测试的示例数据的链接。

每项测试运行六次，首次运行（“冷运行”）的时间已丢弃。 为了允许偶发离群值，剩余五次运行的最长时间也已丢弃。 已使用四次剩余运行的平均值来计算每项测试的平均消耗运行时。 运行每项测试之前已引发 R 垃圾回收。 每项测试的 *rowsPerRead* 值设置为 500000。

## <a name="data-size-when-using-compression-and-a-columnar-store-table"></a>使用压缩和纵栏存储表时的数据大小

下面是使用压缩和纵栏表来减小数据大小的结果：

| 表名 | 行 | 保留 | 数据 | index_size | 未使用 | 节省率（保留） |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| _airlineWithIndex_ | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | 528 KB | 0 |
| _airlineWithPageComp_ | 10000000 | 625784 KB | 623744 KB | 1352 KB | 688 KB | 79% |
| _airlineWithRowComp_ | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| _airlineColumnar_ | 9999999 | 201992 KB | 201624 KB | 不适用 | 368 KB | 93% |

## <a name="using-integer-vs-string-in-formula"></a>在公式中使用整数与字符串

在此试验中，已将 `rxLinMod` 用于两个表，其中一个表包含字符串因子，另一个表包含整数因子。 
+ 对于 _airline_ 表

    *DayOfWeek* 是字符串
    
    `colInfo` 参数用于指定因子级别（`Monday`、`Tuesday`...） 

+ 对于 *airlineWithIndex* 表

    *DayOfWeek* 是整数 

    未指定 `colInfo`
    
在这两种情况下，都使用了同一个公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。 

以下结果明确显示了使用整数而不是字符串作为因子带来的好处：

| 表名 | 测试名称 | 平均时间 |
| ---------- | --------- | ------------ |
| _airline_ | _FactorCol_ | 10.72 |
| _airlineWithIntCol_ | _IntCol_ | 3.4475 |

## <a name="using-compression"></a>使用压缩

在此试验中，已将 `rxLinMod` 用于多个数据表：*airlineWithIndex*、*airlineWithPageComp* 和 *airlineWithRowComp*。 对所有表使用了相同的公式和查询。 

| 表名 | 测试名称 | numTasks | 平均时间 |
| ---------- | --------- | -------- | ------------ |
| _airlineWithIndex_ | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| _airlineWithPageComp_ | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| _airlineWithRowComp_ | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

请注意，单纯使用压缩（*numTasks* 设置为 1）似乎在本示例中起不到作用，因为增大用于处理压缩的 CPU 会抵消 IO 时间的减少。 

但是，如果将 *numTasks* 设置为 4 以便并行运行测试，则平均时间将会减少。 对于较大的数据集，压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要进行试验，确定压缩对数据集产生的影响。

## <a name="avoiding-transformation-function"></a>避免转换函数

在此试验中，已将 `rxLinMod` 用于两次运行中的表 _airlineWithIndex_，其中一次运行使用转换函数，另一次运行未使用转换函数。  

| 测试名称 | 平均时间 |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

请注意，未使用转换函数时（换言之，使用表中预先计算并持久保存的列时），时间已得到改善。 如果还有其他许多的转换并且数据集较大 (> 100M)，则时间节省将明显得多。

## <a name="using-columnar-store"></a>使用纵栏表存储

在此试验中，已将 `rxLinMod` 用于两个表（_airlineWithIndex_ 和 _airlineColumnar_），并且未使用转换。 这些结果表明，纵栏表存储的表现要优于行存储。 在较大的数据集 (> 100 M) 中，产生的性能差异非常明显。  

| 表名 | 测试名称 |平均时间 |
| ---------- | --------- | ------------ |
| _airlineWithIndex_ | RowStore | 4.67 |
| _airlineColumnar_ | ColStore | 4.555 |

## <a name="effect-of-the-cube-parameter"></a>多维数据集参数的影响

在此试验中，已将 `rxLinMod` 用于 _airline_ 表，该表中的列 _DayOfWeek_ 存储为字符串。 使用的公式为 `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`。 结果明确显示使用 `cube` 参数有助于提高性能。 

| 测试名称 | 多维数据集参数 | numTasks | 平均时间 | 单行预测 (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## <a name="effect-of-maxdepth-for-rxdtree"></a>rxDTree 的 maxDepth 影响

在此试验中，已将 `rxDTree` 用于 _airlineColumnar_ 表。 已使用 *maxDepth* 的多个不同值来演示它对运行时复杂性造成的影响。 

| 测试名称 | maxDepth | 平均时间 |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

随着深度增大，节点总数将呈指数组增加，消耗时间也显著增加。 在此项测试中，*numTasks* 设置为 4。

## <a name="effect-of-windows-power-plan-options"></a>Windows 电源计划选项的影响

在此试验中，已将 `rxLinMod` 用于 _airlineWithIntCol_ 表。 Windows 电源计划已设置为“平衡”或“高性能”。 在所有测试轮次中，*numTasks* 设置为 1。 该测试运行了 6 次，并在同时使用两种电源选项的条件下执行了两次，目的是演示使用“平衡”电源选项时结果的变化。 结果表明，使用高性能电源计划时，数字更一致且更快。 

“高性能”电源选项：

| 测试名称 | “运行” # | 占用时间 | 平均时间 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.57 秒 | &nbsp; |
| &nbsp; | 2 | 3.45 秒 | &nbsp; |
| &nbsp; | 3 | 3.45 秒 | &nbsp; |
| &nbsp; | 4 | 3.55 秒 | &nbsp; |
| &nbsp; | 5 | 3.55 秒 | &nbsp; |
| &nbsp; | 6 | 3.45 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3.45 秒 | &nbsp; |
| &nbsp; | 2 | 3.53 秒 | &nbsp; |
| &nbsp; | 3 | 3.63 秒 | &nbsp; |
| &nbsp; | 4 | 3.49 秒 | &nbsp; |
| &nbsp; | 5 | 3.54 秒 | &nbsp; |
| &nbsp; | 6 | 3.47 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

“平衡”电源选项：

| 测试名称 | “运行” # | 占用时间 | 平均时间 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 秒 | &nbsp; |
| &nbsp; | 2 | 4.15 秒 | &nbsp; |
| &nbsp; | 3 | 3.77 秒 | &nbsp; |
| &nbsp; | 4 | 5 秒 | &nbsp; |
| &nbsp; | 5 | 3.92 秒 | &nbsp; |
| &nbsp; | 6 | 3.8 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3.82 秒 | &nbsp; |
| &nbsp; | 2 | 3.84 秒 | &nbsp; |
| &nbsp; | 3 | 3.86 秒 | &nbsp; |
| &nbsp; | 4 | 4.07 秒 | &nbsp; |
| &nbsp; | 5 | 4.86 秒 | &nbsp; |
| &nbsp; | 6 | 3.75 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## <a name="prediction-using-a-stored-model"></a>使用存储模型进行预测

在此试验中，已创建一个模型并将其存储到数据库。 然后从数据库加载存储的模型，并使用内存（本地计算上下文）中的单行数据框架创建预测。 下面显示了训练、保存和加载模型与预测所花费的时间。 。 

| 表名 | 测试名称 | 平均时间（训练模型） | 保存/加载模型花费的时间 |
| ---------- | --------- | ----- | ----- |
| airline | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09（包括预测花费的时间） |

测试结果显示了保存模型所花费的时间，以及加载模型和预测所花费的时间。 显然，这是执行预测的更快方式。 

## <a name="performance-troubleshooting"></a>性能故障排除

本部分所述的测试使用连同 `3` 值一起传递给测试的 *reportProgress* 参数为每次运行生成输出文件。 控制台输出将定向到输出目录中的某个文件。 输出文件包含有关 IO 所用时间、转换时间和计算时间的信息。 这些时间可用于故障排除和诊断。 

然后，测试脚本将处理每次运行的这些时间，以提供各次运行的平均时间。  例如，下面显示了某次运行的示例时间。 主要关注的时间是“总读取时间”（IO 时间）和“转换时间”（设置计算进程所产生的开销）。

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 > [!TIP]
 > 这些测试脚本和技巧也可用于排查在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中使用 rx 分析函数时遇到的问题。
 
## <a name="scripts-and-resources"></a>脚本和资源

+ Github：本案例研究的[示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)
+ 博客：[Reference Implementation of Credit Risk Prediction using R](https://blogs.msdn.microsoft.com/rserver/2017/02/22/credit-risk-prediction/)（使用 R 进行信用风险预测的参考实现）

     一篇性能案例研究，其中包括可下载的源代码。
       
+ [Monitoring R Services using Custom Reports](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)（使用自定义报告监视 R Services）
 
     可在 SQL Server Management Studio 中查看的自定义报告。

 ## <a name="see-also"></a>另请参阅

 
 [SQL Server R Services 性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R Services 的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)

