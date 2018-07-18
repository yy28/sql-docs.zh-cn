---
title: 第 2 课准备 R 教程环境使用 PowerShell （SQL Server 机器学习） |Microsoft 文档
description: 本教程演示如何将 R 嵌入在 SQL Server 中存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1280d7c82d48c8ed596271cd7a73fa13ec1664c7
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249740"
---
# <a name="lesson-2-set-up-the-tutorial-environment-using-powershell"></a>第 2 课： 使用 PowerShell 的教程环境设置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

在此步骤中，你将运行 PowerShell 脚本以创建所需的演练数据库对象。 此脚本创建，并加载使用在上一步中获取的示例数据的数据库。 它还将创建函数和在教程中使用的存储的过程。

## <a name="create-and-load-database-objects"></a>创建并加载数据库对象

在下载的文件中，你应看到的 PowerShell 脚本 (`RunSQL_SQL_Walkthrough.ps1`) 准备演练环境。 脚本执行的操作包括：

- 如果尚未安装，安装 SQL Native Client 和 SQL 命令行实用工具。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。

- 在创建数据库和表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，和大容量插入数据来源于.csv 文件。

- 创建多个 SQL 函数和存储的过程。

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>修改脚本以使用受信任的 Windows 标识

默认情况下，该脚本假设 SQL Server 数据库用户登录名和密码。 如果你在你的 Windows 用户帐户是 db_owner，你可以使用 Windows 标识创建对象。 为此，请打开`RunSQL_SQL_Walkthrough.ps1`在代码编辑器中和追加**`-T`** 到 bcp 大容量插入命令 （行 238）：

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>运行脚本以创建对象

以管理员身份打开 PowerShell 命令提示符并运行以下命令。
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
你将提示您输入的以下信息：

- 服务器实例[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]已安装。 在默认实例中，这可以与计算机名称一样简单。

- 数据库名称。 对于本教程中，脚本假定`TaxiNYC_Sample`。

- 用户名称和用户密码。 输入这些值的 SQL Server 数据库登录名。 或者，如果你修改脚本以接受受信任的 Windows 标识，按 enter 键将这些值保留为空。 连接上使用 Windows 标识。

- 在上一课中下载的示例数据的完全限定的文件名称。 例如： `C:\tempRSQL\nyctaxi1pct.csv`

提供这些值后，立即执行该脚本。 在脚本执行中的所有占位符名称期间[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本会更新，以便使用您提供的输入。

## <a name="review-database-objects"></a>查看数据库对象
   
脚本执行完成后，确认数据库对象上存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 你应看到数据库、 表、 函数和存储的过程。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 如果数据库对象已存在，则无法再次创建。
>   
> 如果表已存在，则会追加数据，而不是将其覆盖。 因此，运行脚本之前请确保删除所有现有对象。

## <a name="objects-used-in-this-tutorial"></a>本教程中使用的对象

下表总结了在本课程中创建的对象。 尽管您仅运行一个 PowerShell 脚本 (`RunSQL_SQL_Walkthrough.ps1`)，该脚本将调用其他的 SQL 脚本，反过来，在数据库中创建对象。 用于创建每个对象的脚本会在描述中提到。

|**对象名称**|**对象类型**|**Description**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | “数据库” |创建由创建-db-tb-上载-data.sql 脚本。 创建一个数据库和两个表：<br /><br />dbo.nyctaxi_sample 表： 包含主 NYC Taxi 数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 NYC Taxi 数据集 1%样本插入到此表。<br /><br />dbo.nyc_taxi_models 表： 用来持久化保存训练的高级的分析模型。|
|**fnCalculateDistance** |标量值函数 (scalar-valued function) | 创建由 fnCalculateDistance.sql 脚本。 计算挑选和 dropoff 位置之间的直接距离。 在其中使用此函数[创建数据功能](../tutorials/sqldev-create-data-features-using-t-sql.md)，[训练和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)和[实施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |表值函数 (table-valued function) | 创建由 fnEngineerFeatures.sql 脚本。 创建新的数据功能，以便为模型定型。 在其中使用此函数[创建数据功能](../tutorials/sqldev-create-data-features-using-t-sql.md)和[实施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**PlotHistogram** |存储过程 | 创建由 PlotHistogram.sql 脚本。 调用要绘制的变量直方图的 R 函数，然后返回作为二进制对象绘图。 此存储的过程用于在[浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)。|
|**PlotInOutputFiles** |存储过程| 创建由 PlotInOutputFiles.sql 脚本。 创建使用 R 函数的图形，并将保存为本地的 PDF 文件的输出。 此存储的过程用于在[浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)。|
|**PersistModel** |存储过程 | 创建由 PersistModel.sql 脚本。 将已序列化在 varbinary 数据类型，并将其写入指定的表的模型。 |
|**PredictTip**  |存储过程 |创建由 PredictTip.sql 脚本。 调用经过训练的模型使用模型创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。 此存储的过程用于在[实施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**PredictTipSingleMode**  |存储过程| 创建由 PredictTipSingleMode.sql 脚本。 调用经过训练的模型使用模型创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。 此存储的过程用于在[实施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**TrainTipPredictionModel**  |存储过程|创建由 TrainTipPredictionModel.sql 脚本。 通过调用 R 程序包训练逻辑回归模型。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。 此存储的过程用于在[训练和保存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|

## <a name="next-lesson"></a>下一课

[第 3 课： 浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>上一课

[第 1 课： 下载示例数据](../tutorials/sqldev-download-the-sample-data.md)
