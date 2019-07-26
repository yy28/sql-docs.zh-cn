---
title: 下载适用于嵌入式 R 和 Python 的 NYC 出租车演示数据和脚本
description: 下载纽约出租车示例数据和创建数据库的说明。 数据用于 SQL Server Python 和 R 语言教程, 这些教程显示了如何在 SQL Server 存储过程和 T-sql 函数中嵌入脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d5d74090713666a2da6058d9eccee1e33e4d7cb
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469747"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 教程的 NYC 出租车演示数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何设置一个示例数据库, 其中包含来自[纽约出租车和礼车委员会](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)的公共数据。 此数据在多个 R 和 Python 教程中用于 SQL Server 上的数据库内分析。 为了使示例代码运行速度更快, 我们创建了一个代表性 1% 的数据采样。 在您的系统上, 数据库备份文件略微超过 90 MB, 在主数据表中提供1700000行。

若要完成此练习, 您应该有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或其他可还原数据库备份文件和运行 t-sql 查询的工具。

使用此数据集的教程和快速入门包括:

+ [使用 SQL Server 中的 R 了解数据库内分析](sqldev-in-database-r-for-sql-developers.md)
+ [使用 SQL Server 中的 Python 了解数据库内分析](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>下载文件

该示例数据库是 Microsoft 托管的 SQL Server 2016 .BAK 文件。 可以在2016和更高版本上还原 SQL Server。 单击链接时, 将立即开始下载文件。 

文件大小约为 90 MB。

1. 单击 " [NYCTaxi_Sample](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) " 下载数据库备份文件。

2. 将该文件复制到 C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup 文件夹。

3. 在 Management Studio 中, 右键单击 "**数据库**", 然后选择 "**还原文件和文件组**"。

4. 输入*NYCTaxi_Sample*作为数据库名称。

5. 单击 "**来自设备**", 然后打开 "文件选择" 页以选择备份文件。 单击 "**添加**" 以选择 "NYCTaxi_Sample"。

6. 选择 "**还原**" 复选框, 然后单击 **"确定"** 以还原数据库。

## <a name="review-database-objects"></a>查看数据库对象
   
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]确认实例上存在数据库对象。 应会看到数据库、表、函数和存储过程。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 数据库中的对象

下表总结了 NYC 出租车 demo 数据库中创建的对象。

|**对象名称**|**对象类型**|**说明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | “数据库” | 创建一个数据库和两个表：<br /><br />nyctaxi_sample 表:包含主 NYC 出租车数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 NYC 出租车数据集的 1% 样本插入到此表中。<br /><br />nyc _taxi_models 表:用于保留训练的高级分析模型。|
|**fnCalculateDistance** |标量值函数 (scalar-valued function) | 计算拾取和下车位置之间的直接距离。 此函数用于[创建数据功能](sqldev-create-data-features-using-t-sql.md)、[定型和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)以及[操作 R 模型](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |表值函数 (table-valued function) | 为模型定型创建新的数据功能。 此函数用于[创建数据功能](sqldev-create-data-features-using-t-sql.md)和[操作 R 模型](sqldev-operationalize-the-model.md)。|


使用在各种教程中找到的 R 和 Python 脚本来创建存储过程。 下表总结了从不同课程运行脚本时, 可以选择添加到 NYC 出租车演示程序的存储过程。

|**存储过程**|**语言**|**说明**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 调用 RevoScaleR rxHistogram 函数以绘制变量的直方图, 然后将该绘图作为二进制对象返回。 此存储过程用于[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**RPlotRHist** |R| 使用他函数创建图形, 并将输出保存为本地 PDF 文件。 此存储过程用于[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**RxTrainLogitModel**  |R| 通过调用 R 包训练逻辑回归模型。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。 此存储过程用于[定型并保存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|
|**RxPredictBatchOutput**  |R | 调用定型模型来使用模型创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。 此存储过程用于[预测潜在的结果](sqldev-operationalize-the-model.md)。|
|**RxPredictSingleRow**  |R| 调用定型模型来使用模型创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。 此存储过程用于[预测潜在的结果](sqldev-operationalize-the-model.md)。|

## <a name="query-the-data"></a>查询数据

作为验证步骤, 运行查询以确认已上传数据。

1. 在对象资源管理器的 "数据库" 下, 右键单击**NYCTaxi_Sample**数据库, 然后启动一个新查询。

2. 运行一些简单的查询:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
数据库包含1700000行。

3. 数据库中包含数据集的**nyctaxi_sample**表。 该表已针对基于集的计算进行了优化, 并添加了[列存储索引](../../relational-databases/indexes/columnstore-indexes-overview.md)。 运行此语句可生成表的快速摘要。

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
结果应类似于以下屏幕截图中显示的结果。

  ![表摘要信息](media/nyctaxidatatablesummary.png "查询结果")

## <a name="next-steps"></a>后续步骤

NYC 出租车示例数据现在可用于实际操作。

+ [使用 SQL Server 中的 R 了解数据库内分析](sqldev-in-database-r-for-sql-developers.md)
+ [使用 SQL Server 中的 Python 了解数据库内分析](sqldev-in-database-python-for-sql-developers.md)