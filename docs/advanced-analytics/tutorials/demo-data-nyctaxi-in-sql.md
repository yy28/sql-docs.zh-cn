---
title: 下载适用于嵌入的 R 和 Python-SQL Server 机器学习的 NYC 出租车演示数据和脚本
description: 有关下载纽约市出租车示例数据和创建数据库的说明。 在 SQL Server Python 和 R 语言教程显示如何在 SQL Server 存储过程和 T-SQL 函数中嵌入脚本中使用数据。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 502f46b67dbf282a7b3daeac76882915a7c3ac84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "64505450"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>NYC 出租车演示数据的 SQL Server Python 和 R 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何设置由从公共数据组成的一个示例数据库[纽约市出租车和礼车委员会](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)。 在多个 R 和 Python 的教程中的 SQL Server 上的数据库内分析使用此数据。 若要使示例代码更快地运行，我们创建了具有代表性的 1%抽样数据。 在系统上的数据库备份文件是略微超过 90 MB，提供在主要数据表中的 1.7 万行。

若要完成此练习中，您应有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或另一个工具，可以还原数据库备份文件和运行 T-SQL 查询。

教程和快速入门使用此数据集包括：

+ [了解在 SQL Server 中使用 R 的数据库内分析](sqldev-in-database-r-for-sql-developers.md)
+ [了解数据库内分析在 SQL Server 中使用 Python](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>下载文件

示例数据库是由 Microsoft 托管的 SQL Server 2016 BAK 文件。 SQL Server 2016 及更高版本时，可以将其还原。 立即单击链接开始下载文件。 

文件大小为约 90 MB。

1. 单击[NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)下载数据库备份文件。

2. 将文件复制到 C:\Program files\Microsoft SQL Server\MSSQL 实例 name\MSSQL\Backup 文件夹。

3. 在 Management Studio 中，右键单击**数据库**，然后选择**还原文件和文件组**。

4. 输入*NYCTaxi_Sample*作为数据库名称。

5. 单击**从设备**，然后打开文件选择页以选择备份文件。 单击**添加**选择 NYCTaxi_Sample.bak。

6. 选择**还原**复选框，单击**确定**还原数据库。

## <a name="review-database-objects"></a>查看数据库对象
   
确认数据库对象上存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您应看到数据库、 表、 函数和存储的过程。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 数据库中的对象

下表总结了在 NYC 出租车演示数据库中创建的对象。

|**对象名称**|**对象类型**|**说明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | “数据库” | 创建一个数据库和两个表：<br /><br />dbo.nyctaxi_sample 表：包含主 NYC 出租车数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 NYC 出租车数据集 1%样本插入此表。<br /><br />dbo.nyc_taxi_models 表：用于保存已训练的高级的分析模型。|
|**fnCalculateDistance** |标量值函数 (scalar-valued function) | 计算上车和下车位置之间的直接距离。 在使用此函数[创建数据功能](sqldev-create-data-features-using-t-sql.md)，[训练和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)并[操作 R 模型](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |表值函数 (table-valued function) | 创建新的数据功能，用于为模型定型。 在使用此函数[创建数据功能](sqldev-create-data-features-using-t-sql.md)并[实施 R 模型](sqldev-operationalize-the-model.md)。|


使用 R 和 Python 脚本找到各种教程中创建的存储的过程。 下表总结了从多个课程运行脚本时可以选择添加对 NYC 出租车演示数据库的存储的过程。

|**存储的过程**|**语言**|**说明**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 调用 RevoScaleR rxHistogram 函数绘制变量的直方图，然后返回将绘图作为二进制对象。 在使用此存储的过程[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**RPlotRHist** |R| 创建使用 Hist 函数的图形，并将输出保存为本地 PDF 文件。 在使用此存储的过程[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**RxTrainLogitModel**  |R| 通过调用 R 包定型逻辑回归模型。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。 在使用此存储的过程[训练和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|
|**RxPredictBatchOutput**  |R | 调用训练的模型以使用该模型创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。 在使用此存储的过程[预测潜在结果](sqldev-operationalize-the-model.md)。|
|**RxPredictSingleRow**  |R| 调用训练的模型以使用该模型创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。 在使用此存储的过程[预测潜在结果](sqldev-operationalize-the-model.md)。|

## <a name="query-the-data"></a>查询数据

作为验证步骤，运行查询以确认数据已上传。

1. 在对象资源管理器，在数据库中右键单击**NYCTaxi_Sample**数据库，然后启动一个新查询。

2. 运行一些简单的查询：

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
数据库包含 1.7 万行。

3. 在数据库中是**nyctaxi_sample**包含数据集的表。 已针对通过添加基于集的计算进行优化的表[列存储索引](../../relational-databases/indexes/columnstore-indexes-overview.md)。 运行此语句生成表上的快速摘要。

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
结果应类似于以下屏幕截图中显示。

  ![表的摘要信息](media/nyctaxidatatablesummary.png "查询结果")

## <a name="next-steps"></a>后续步骤

NYC 出租车示例数据现已可供动手学习。

+ [了解在 SQL Server 中使用 R 的数据库内分析](sqldev-in-database-r-for-sql-developers.md)
+ [了解数据库内分析在 SQL Server 中使用 Python](sqldev-in-database-python-for-sql-developers.md)