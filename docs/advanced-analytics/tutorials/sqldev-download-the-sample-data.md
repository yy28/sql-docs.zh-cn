---
title: 下载 NYC 出租车演示数据和脚本适用于嵌入的 R 和 Python （SQL Server 机器学习） |Microsoft Docs
description: 有关下载纽约市出租车示例数据和创建数据库的说明。 在 SQL Server 教程演示如何嵌入 R 中使用数据和 Python 在 SQL Server 存储过程和 T-SQL 的函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7420476b20cef612c45227f66497ae554def7b1d
ms.sourcegitcommit: 9d0ff4f3e40db48fc01788684d34719065d159b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "44724331"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>适用于 SQL Server 的 NYC 出租车演示数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文为教程，介绍如何使用 SQL Server 中的数据库内分析 R 和 Python 准备您的系统。

在此练习中，将下载示例数据，用于准备环境的 PowerShell 脚本和[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本在多个教程中使用的文件。 完成后， **NYCTaxi_Sample**有可用的本地实例，提供演示数据获得第一手学习数据库。 

## <a name="prerequisites"></a>必要條件

你将需要 internet 连接、 PowerShell 和在计算机上的本地管理权限。 您应该[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或其他工具来验证对象创建。

## <a name="download-nyc-taxi-demo-data-and-scripts-from-github"></a>从 Github 下载 NYC 出租车演示数据和脚本

1.  打开 Windows PowerShell 命令控制台。
  
    使用**以管理员身份运行**选项来创建目标目录或文件写入指定的目标。
  
2.  运行以下 PowerShell 命令，将参数 DestDir 的值更改为任何本地目录。 此处使用的默认值是“TempRSQL”。
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    如果 DestDir 中指定的文件夹不存在，则可以通过 PowerShell 脚本创建。
  
    > [!TIP]
    > 如果遇到错误，可以暂时将设置为 PowerShell 脚本执行策略**不受限制**仅用于本次演练通过使用 Bypass 参数并将当前会话更改范围。
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > 运行此命令不会导致配置更改。
  
    根据 Internet 连接，下载可能需要一段时间。
  
3.  已下载的所有文件，PowerShell 脚本将打开到*DestDir*文件夹。 在 PowerShell 命令提示符中，运行以下命令并查看已下载的文件。
  
    ```
    ls
    ```
  
    **结果：**
  
    ![通过 PowerShell 脚本下载的文件列表](media/rsql-devtut-filelist.png "通过 PowerShell 脚本下载的文件列表")

## <a name="create-nyctaxisample-database"></a>创建 NYCTaxi_Sample 数据库

在下载的文件，您应该看到 PowerShell 脚本 (**RunSQL_SQL_Walkthrough.ps1**) 创建一个数据库和大容量加载数据。 脚本执行的操作包括：

+ 如果尚未安装，安装 SQL Native Client 和 SQL 命令行实用工具。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。

+ 创建一个数据库和表上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，并大容量插入数据源从.csv 文件。

+ 创建多个 SQL 函数和多个教程中使用的存储的过程。

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>修改脚本以使用受信任的 Windows 标识

默认情况下，此脚本假定 SQL Server 数据库用户登录名和密码。 如果您在您的 Windows 用户帐户是 db_owner，可以使用 Windows 标识创建的对象。 若要执行此操作，打开`RunSQL_SQL_Walkthrough.ps1`代码编辑器中并将追加**`-T`** 到 bcp 大容量插入命令 （行 238）：

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>运行脚本，以创建对象

使用管理员 PowerShell C:\tempRSQL，在命令提示符下运行以下命令。
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
系统会提示输入以下信息：

- 服务器实例[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]已安装。 在默认实例，这可以很简单，只需为计算机名称。

- 数据库名称。 对于本教程中，脚本假定`NYCTaxi_Sample`。

- 用户名和用户密码。 输入这些值的 SQL Server 数据库登录名。 或者，如果您修改了脚本，以接受受信任的 Windows 标识，则按 Enter 将这些值保留为空。 在连接上使用 Windows 标识。

- 在上一课中下载的示例数据的完全限定的文件名。 例如： `C:\tempRSQL\nyctaxi1pct.csv`

提供这些值后，立即执行该脚本。 脚本在执行期间中的所有占位符名称[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本已更新为使用你提供的输入。

## <a name="review-database-objects"></a>查看数据库对象
   
脚本执行完成后，确认数据库对象上存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您应看到数据库、 表、 函数和存储的过程。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 如果数据库对象已存在，则无法再次创建。
>   
> 如果表已存在，则会追加数据，而不是将其覆盖。 因此，运行脚本之前请确保删除所有现有对象。

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 数据库中的对象

下表总结了在 NYC 出租车演示数据库中创建的对象。 尽管只能运行一个 PowerShell 脚本 (`RunSQL_SQL_Walkthrough.ps1`)，该脚本会调用其他 SQL 脚本又以在数据库中创建的对象。 在说明中提到了用于创建每个对象的脚本。

|**对象名称**|**对象类型**|**Description**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | “数据库” |创建由创建-db-tb-上传-data.sql 脚本。 创建一个数据库和两个表：<br /><br />dbo.nyctaxi_sample 表： 包含主 NYC 出租车数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 NYC 出租车数据集 1%样本插入此表。<br /><br />dbo.nyc_taxi_models 表： 用于保存已训练的高级的分析模型。|
|**fnCalculateDistance** |标量值函数 (scalar-valued function) | 创建由 fnCalculateDistance.sql 脚本。 计算上车和下车位置之间的直接距离。 在使用此函数[创建数据功能](sqldev-create-data-features-using-t-sql.md)，[训练和保存模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)并[操作 R 模型](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |表值函数 (table-valued function) | 创建由 fnEngineerFeatures.sql 脚本。 创建新的数据功能，用于为模型定型。 在使用此函数[创建数据功能](sqldev-create-data-features-using-t-sql.md)并[实施 R 模型](sqldev-operationalize-the-model.md)。|
|**PlotHistogram** |存储过程 | 创建由 PlotHistogram.sql 脚本。 调用 R 函数绘制变量的直方图，然后返回将绘图作为二进制对象。 在使用此存储的过程[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**PlotInOutputFiles** |存储过程| 创建由 PlotInOutputFiles.sql 脚本。 创建使用 R 函数的图形，然后将输出保存为本地 PDF 文件。 在使用此存储的过程[浏览和可视化数据](sqldev-explore-and-visualize-the-data.md)。|
|**PersistModel** |存储过程 | 创建由 PersistModel.sql 脚本。 将已序列化数据类型为 varbinary，并将其写入到指定的表的模型。 |
|**PredictTip**  |存储过程 |创建由 PredictTip.sql 脚本。 调用训练的模型以使用该模型创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。 在使用此存储的过程[使 R 模型可操作化](sqldev-operationalize-the-model.md)。|
|**PredictTipSingleMode**  |存储过程| 创建由 PredictTipSingleMode.sql 脚本。 调用训练的模型以使用该模型创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。 在使用此存储的过程[使 R 模型可操作化](sqldev-operationalize-the-model.md)。|
|**TrainTipPredictionModel**  |存储过程|创建由 TrainTipPredictionModel.sql 脚本。 通过调用 R 包定型逻辑回归模型。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。 在使用此存储的过程[训练和保存模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)。|

## <a name="next-steps"></a>后续步骤

NYC 出租车示例数据现已可供动手学习。

+ [了解在 SQL Server 中使用 R 的数据库内分析](sqldev-in-database-r-for-sql-developers.md)