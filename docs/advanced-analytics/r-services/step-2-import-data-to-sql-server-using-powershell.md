---
title: "步骤 2：使用 PowerShell 将数据导入 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8a43f340803c0a8be69b346c3922bcc705ee6c22
ms.lasthandoff: 04/11/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步骤 2：使用 PowerShell 将数据导入 SQL Server
此步骤将运行一个下载的脚本，创建演练所需的数据库对象。 该脚本还会创建大多数将使用的存储过程，并将示例数据上传到指定的数据库中的表。  
  
## <a name="run-the-scripts-to-create-sql-objects"></a>运行脚本创建 SQL 对象  
在下载的文件中，可以看到一个 PowerShell 脚本。 运行此脚本，准备用于演练的环境。  
  
脚本执行的操作包括：  
  
-   如果尚未安装 SQL Native Client 和 SQL 命令行实用程序，请先安装。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上创建数据库和表，并将数据大容量插入到表中。  
  
-   创建多个 SQL 函数和存储过程。  
  
#### <a name="to-run-the-script"></a>运行该脚本  
1.  以管理员身份打开 PowerShell 命令提示符并运行以下命令。  
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  
  
    系统将提示输入以下信息：  
  
    -   安装有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例的名称或地址  
  
    -   实例上某帐户的用户名和密码。 使用的帐户必须能够创建数据库、创建表和存储过程，以及将数据上传到表。  
  
    -   刚下载的示例数据文件的路径和文件名。 例如：  
  
        `C:\tempRSQL\nyctaxi1pct.csv`  
  
2.  在此步骤中，还需修改所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，以作为脚本输入提供的数据库名称和用户名替换占位符。  
  
    花一些时间查看脚本创建的存储过程和函数。  
  
    |||  
    |-|-|  
    |**SQL 脚本文件名**|**函数**|  
    |create-db-tb-upload-data.sql|创建一个数据库和两个表：<br /><br />nyctaxi_sample：包含主 NYC Taxi 数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 将在此表中插入 1% 的 NYC Taxi 数据集示例。<br /><br />nyc_taxi_models：用于保留已定型的高级分析模型。|  
    |fnCalculateDistance.sql|创建标量值函数，用于计算搭乘位置和下车位置之间直接距离|  
    |fnEngineerFeatures.sql|创建表值函数，用于为模型定型创建新的数据功能|  
    |PersistModel.sql|创建可调用来保存模型的存储过程。 存储过程带有一个已序列化的、数据类型为 varbinary 的模型，并将此模型写入指定的表。|  
    |PredictTipBatchMode.sql|创建一个存储过程，此存储过程调用定型模型，并用其创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。|  
    |PredictTipSingleMode.sql|创建一个存储过程，此存储过程调用定型模型，并用其创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。|  
  
    在本演练中的后半部分中，将创建一些附加的存储过程：  
  
    |||  
    |-|-|  
    |**SQL 脚本文件名**|**函数**|  
    |PlotHistogram.sql|创建用于数据浏览的存储过程。 此存储过程调用 R 函数绘制变量的直方图，然后将绘图作为二进制对象返回。|  
    |PlotInOutputFiles.sql|创建用于数据浏览的存储过程。 此存储过程使用 R 函数创建图形，然后将输出保存为本地 PDF 文件。|  
    |TrainTipPredictionModel.sql|创建可通过调用 R 包定型逻辑回归模型的存储过程。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|  
  
3.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和指定的登录名登录到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例，验证是否可以看到创建的数据库、表、函数和存储过程。  
  
    ![rsql_devtut_BrowseTables](../../advanced-analytics/r-services/media/rsql-devtut-browsetables.PNG "rsql_devtut_BrowseTables")  
  
    > [!NOTE]  
    > 如果数据库对象已存在，则无法再次创建。  
    >   
    > 如果表已存在，则会追加数据，而不是将其覆盖。 因此，运行脚本之前请确保删除所有现有对象。  
  
## <a name="next-step"></a>下一步  
[步骤 3：浏览和可视化数据](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)  
  
## <a name="previous-step"></a>上一步  
[步骤 1：下载示例数据](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  


