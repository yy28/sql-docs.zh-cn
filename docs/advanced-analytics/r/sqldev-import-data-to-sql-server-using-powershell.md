---
title: "第 2 课： 将数据导入到 SQL Server 使用 PowerShell |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c9190157b005158bb2ca8b9aeb7addbdbf1e69f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-2-import-data-to-sql-server-using-powershell"></a>第 2 课： 将数据导入到 SQL Server 使用 PowerShell

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

此步骤将运行一个下载的脚本，创建演练所需的数据库对象。 该脚本还会创建大多数将使用的存储过程，并将示例数据上传到指定的数据库中的表。

## <a name="run-the-scripts-to-create-sql-objects"></a>运行用于创建 SQL 对象的脚本

在下载的文件中，你应看到可运行以准备演练环境的 PowerShell 脚本。 脚本执行的操作包括：

- 如果尚未安装 SQL Native Client 和 SQL 命令行实用程序，请先安装。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。

- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上创建数据库和表，并将数据大容量插入到表中。

- 创建多个 SQL 函数和存储过程。

### <a name="run-the-script"></a>运行脚本

1.  以管理员身份打开 PowerShell 命令提示符并运行以下命令。
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```
  
    系统将提示输入以下信息：
  
    - 安装有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例的名称或地址
  
    - 实例上某帐户的用户名和密码。 该帐户必须有权创建数据库、 创建表和存储的过程，并将数据上载到表。 如果未提供的用户名和密码，你的 Windows 标识用于登录到 SQL Server。
  
    - 刚下载的示例数据文件的路径和文件名。 例如：
  
        `C:\tempRSQL\nyctaxi1pct.csv`
  
2.  在此步骤中，还需修改所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，以作为脚本输入提供的数据库名称和用户名替换占位符。
  
    花一些时间查看脚本创建的存储过程和函数。
  
    |**SQL 脚本文件名**|**函数**|
    |-|-|
    |create-db-tb-upload-data.sql|创建一个数据库和两个表：<br /><br />nyctaxi_sample：包含主 NYC Taxi 数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 将在此表中插入 1% 的 NYC Taxi 数据集示例。<br /><br />nyc_taxi_models：用于保留已定型的高级分析模型。|
    |fnCalculateDistance.sql|创建标量值函数，用于计算搭乘位置和下车位置之间直接距离|
    |fnEngineerFeatures.sql|创建表值函数，用于为模型定型创建新的数据功能|
    |PersistModel.sql|创建可调用来保存模型的存储过程。 存储过程带有一个已序列化的、数据类型为 varbinary 的模型，并将此模型写入指定的表。|
    |PredictTipBatchMode.sql|创建一个存储过程，此存储过程调用定型模型，并用其创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。|
    |PredictTipSingleMode.sql|创建一个存储过程，此存储过程调用定型模型，并用其创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。|
  
    在本演练中的后半部分中，将创建一些附加的存储过程：
  
    |**SQL 脚本文件名**|**函数**|
    |------|------|
    |PlotHistogram.sql|创建用于数据浏览的存储过程。 此存储过程调用 R 函数绘制变量的直方图，然后将绘图作为二进制对象返回。|
    |PlotInOutputFiles.sql|创建用于数据浏览的存储过程。 此存储过程使用 R 函数创建图形，然后将输出保存为本地 PDF 文件。|
    |TrainTipPredictionModel.sql|创建可通过调用 R 包定型逻辑回归模型的存储过程。 该模型预测附属列的值，并使用随机选择的 70% 的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|
  
3.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和指定的登录名登录到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例，验证是否可以看到创建的数据库、表、函数和存储过程。
  
    ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")
  
    > [!NOTE]
    > 如果数据库对象已存在，则无法再次创建。
    >   
    > 如果表已存在，则会追加数据，而不是将其覆盖。 因此，运行脚本之前请确保删除所有现有对象。

## <a name="next-lesson"></a>下一课

[第 3 课： 浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>上一课

[第 1 课： 下载示例数据](../tutorials/sqldev-download-the-sample-data.md)
