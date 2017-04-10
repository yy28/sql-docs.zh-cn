---
title: "性能案例研究 (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# 性能案例研究 (R Services)

为了演示前面各节中提供的指南的效果，运行了测试使用从航空公司数据集中的表。 

## 测试和示例数据

有六个表，但是有 10 米每个表中的行︰

| 表名 | Description |
| ---------- | ----------- |
| _航空公司_ | 数据从原始 xdf 文件中使用转换 *rxDataStep*。 |
| _airlineWithIntCol_ | *DayOfWeek* 转换为一个整数，而不是字符串。 此外添加了 *rowNum* 列。 |
| _airlineWithIndex_ | 与相同的数据 *airlineWithIntCol* 表中，但与单个聚集的索引使用 *rowNum* 列。 |
| _airlineWithPageComp_ | 与相同的数据 *airlineWithIndex* 表中，但使用页压缩已启用。 此外添加了两个列 *CRSDepHour* 和 *Late*, ，其计算出 *CRSDepTime* 和 *ArrDelay*。 |
| _airlineWithRowComp_ | 与相同的数据 *airlineWithIndex* 表中，但启用行压缩。 此外添加了两个列 *CRSDepHour* 和 *Late* 计算出 *CRSDepTime* 和 *ArrDelay*。 
| _airlineColumnar_ | 纵栏式使用的单个聚集索引的存储区。 此表中填充从清理 csv 文件。 |

用于执行此部分中，以及用于执行测试时，示例数据的链接中描述的测试脚本都是可用在 [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

每个测试运行六次，第一次运行 (cold 运行，请) 的时间而被丢弃。 若要允许偶尔离群值，还删除剩余的五个运行的最长时间。 计算每个测试的平均已用运行时所花的四个剩余运行的平均值。 每个测试之前引发 R 垃圾回收。 值 *rowsPerRead* 为每个测试设置为 500000。

## 使用压缩和纵栏式存储表时的数据大小

以下是使用压缩和纵栏式表来减小数据大小的结果︰

| 表名 | 行 | 保留 | 数据 | index_size | 未使用 | %保存 （保留） |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | 528 KB | 0 |
| airlineWithPageComp | 10000000 | 625784 KB | 623744 KB | 1352 KB | 688 KB | 79% |
| airlineWithRowComp | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| airlineColumnar | 9999999 | 201992 KB | 201624 KB | n/a | 368 KB | 93% |

## 使用整数 vs。在公式中的字符串

在此实验中， `rxLinMod` 航空公司表使用 (其中 *DayOfWeek* 是一个字符串) 和 *airlineWithIndex* (其中 *DayOfWeek* 是一个整数)。 对于第一种情况， `colInfo` 用于指定因子级别 (`Monday`, ，`Tuesday`, ，...)。 为第二种 `colInfo` 未指定。 在这两种情况下，使用同一个公式。 使用的公式是 `ArrDelay ~ CRSDepTime + DayOfWeek`。 下面的结果清楚地显示出使用整数 vs 字符串的好处︰

| 表名 | 测试名称 | 平均时间 |
| ---------- | --------- | ------------ |
| 航空公司 | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## 使用压缩

在此实验中， `rxLinMod` 与用于 *airlineWithIndex*, ，*airlineWithPageComp*, ，和 *airlineWithRowComp* 表。 所有表都使用相同的公式和查询。 

| 表名 | 测试名称 | numTasks | 平均时间 |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

请注意该单独的压缩 (*numTasks* 设置为 1，) 似乎未帮助在此示例中，如 CPU 来处理压缩的增加来减少 IO time 补偿。 但是，测试运行时并行通过设置 *numTasks* 为 4，平均时间将缩短。 对于较大的数据集的压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要试验来确定效果压缩对数据集。

## 避免转换函数

在此实验中， `rxLinMod` 用于 airlineWithIndex 表使用或不使用转换函数。  

| 测试名称 | 平均时间 |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

请注意，没有时间缩短不使用 （使用预计算并保留在表中的列） 的转换函数时。 如果有很多更多的转换和数据集，则较大 （> 100 米），节省的空间将会大得多。

## 使用纵栏式应用商店

在此实验中， `rxLinMod` 所用的 airlineWithIndex 和 airlineColumnar 表而无需使用任何转换。 结果表明纵栏式存储可以比行存储区的更好地执行。 将大型数据集 （> 100 米） 的性能具有明显的差异。  

| 表名 | 测试名称 |平均时间 |
| ---------- | --------- | ------------ |
| airlineWithIndex | 行存储 | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## 多维数据集参数的效果

在此实验中， `rxLinMod` 航空公司表使用其中 `DayOfWeek` 作为字符串存储。 使用的公式是 `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`。 结果清晰地表明，使用 `cube` 参数帮助提高性能。 

| 测试名称 | 多维数据集参数 | numTasks | 平均时间 | 对应的一行预测 (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## 有关 rxDTree maxDepth 的效果

在此实验中， `rxDTree` airlineColumnar 表中使用。 几个不同值的 *maxDepth* 用来演示它如何影响运行的时的复杂性。 随着深度的增加，成指数增加的节点的总数和所用时间会显著增加。 对于此测试 *numTasks* 设置为 4。

| 测试名称 | maxDepth | 平均时间 |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## 电源选项的效果

在此实验中， `rxLinMod` 同时，Windows 已设置为平衡以及高性能电源选项 airlineWithIntCol 表使用。 对于所有测试， *numTasks* 设置为 1。 测试运行的 6 倍，以及在这两个电源选项，以演示的可变性的结果时使用了平衡的电源选项下，两次执行。 结果显示的数字是更加一致和高性能电源选项更快。 

__高性能__ 电源选项︰

| 测试名称 | 运行 # | 占用时间 | 平均时间 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.57 （秒) | &nbsp; |
| &nbsp; | 2 | 为 3.45 （秒) | &nbsp; |
| &nbsp; | 3 | 为 3.45 （秒) | &nbsp; |
| &nbsp; | 4 | 3.55 （秒) | &nbsp; |
| &nbsp; | 5 | 3.55 （秒) | &nbsp; |
| &nbsp; | 6 | 为 3.45 （秒) | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 为 3.45 （秒) | &nbsp; |
| &nbsp; | 2 | 3.53 （秒) | &nbsp; |
| &nbsp; | 3 | 3.63 （秒) | &nbsp; |
| &nbsp; | 4 | 3.49 （秒) | &nbsp; |
| &nbsp; | 5 | 3.54 （秒) | &nbsp; |
| &nbsp; | 6 | 3.47 （秒) | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__平衡__ 电源选项︰

| 测试名称 | 运行 # | 占用时间 | 平均时间 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 （秒) | &nbsp; |
| &nbsp; | 2 | 4.15 （秒) | &nbsp; |
| &nbsp; | 3 | 3.77 （秒) | &nbsp; |
| &nbsp; | 4 | 5 秒 | &nbsp; |
| &nbsp; | 5 | 3.92 （秒) | &nbsp; |
| &nbsp; | 6 | 3.8 （秒) | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3.82 （秒) | &nbsp; |
| &nbsp; | 2 | 3.84 （秒) | &nbsp; |
| &nbsp; | 3 | 3.86 （秒) | &nbsp; |
| &nbsp; | 4 | 4.07 （秒) | &nbsp; |
| &nbsp; | 5 | 4.86 （秒) | &nbsp; |
| &nbsp; | 6 | 3.75 （秒) | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## 使用存储的模型的预测

在此实验中，一个模型是创建并存储到数据库。 然后从数据库和创建使用内存 （本地计算上下文） 中的一行数据帧的预测加载存储的模型。 定型、 保存和加载模型和预测所花费的时间如下所示。 这显然是一种更快的方式来完成预测。 测试结果显示的时间来保存该模型并将模型加载并预测所花费的时间。 

| 表名 | 测试名称 | 平均时间 （以训练模型） | 若要保存/加载模型的时间 |
| ---------- | --------- | ----- | ----- |
| 航空公司 | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09 （包括要预测的时间） |


## 性能故障排除

本部分中使用的测试生成输出文件的每次运行使用 *reportProgress* 参数，传递给具有值测试 `3`。 控制台输出定向到输出目录中的文件。 输出文件包含有关 IO、 过渡时间和计算时间中所用的时间信息。 这些时间可用于故障排除和诊断。 测试脚本处理通过运行拿出的平均时间在各种运行这些时间。 这些测试脚本和技术也可在解决问题，在使用 rx 分析函数时您 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 例如，下面的示例演示一个运行的示例时间。 感兴趣的主要计时是读取时间 （IO 时间） 的总数和过渡时间 （开销以设置用于计算的过程）。

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
 
 ## 另请参阅
 [SQL Server R 服务性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 服务的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)