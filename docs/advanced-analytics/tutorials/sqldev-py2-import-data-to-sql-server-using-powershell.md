---
title: "步骤 2： 将数据导入到 SQL Server 使用 PowerShell |Microsoft 文档"
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 0bee2bcdee8eb5b46d59e43699399fa68cdf3d24
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步骤 2： 将数据导入到 SQL Server 使用 PowerShell

使用本教程，本文摘自[SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，你运行下载的脚本，以创建所需的演练数据库对象之一。 该脚本还会创建多个存储的过程，并将示例数据上载到你指定的数据库中的表。

## <a name="create-database-objects-and-load-data"></a>创建数据库对象和加载数据

在下载的文件之间，你应看到的 PowerShell 脚本， `RunSQL_SQL_Walkthrough.ps1`。 此脚本的目的是准备演练环境。

该脚本执行以下操作：

- 如果尚未安装，安装 SQL Native Client 和 SQL 命令行实用工具。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。

- 上创建一个数据库和表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，并向表中的大容量插入数据。

- 创建多个 SQL 函数和存储的过程。

如果遇到问题，可以作为引用使用脚本来手动执行的步骤。

1. 以管理员身份打开 PowerShell 命令提示符。 如果你尚不在上一步中创建的文件夹中，导航到文件夹，，，然后运行以下命令：
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. 该脚本将提示输入以下信息：

    - 名称或地址[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]已安装与 Python 的机器学习服务实例。
    - 实例上某帐户的用户名和密码。 你使用的帐户必须具有创建数据库、 创建表和存储的过程和大容量加载到表的数据的能力。 
    - 如果未提供的用户名和密码，你的 Windows 标识可用于登录到 SQL Server，并将提升到输入密码。
    - 刚下载的示例数据文件的路径和文件名。 例如，使用 IPv4 地址 `C:\temp\pysql\nyctaxi1pct.csv`

    > [!NOTE]
    > 若要成功加载数据，库 xmlrw.dll 必须是 bcp.exe 所在的文件夹。

3. 该脚本还会修改[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本之前，下载并替换占位符替换为数据库名称和用户名称提供。
  
4. 完成脚本后，登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例使用指定的登录名你，以验证，该数据库，表、 函数和已创建的存储的过程。 下图显示中的对象[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。

    ![浏览在 SSMS 中的表](media/sqldev-python-browsetables1.png "在 SSMS 中查看表")

    > [!NOTE]
    > 如果数据库对象已存在，无法再次创建它们。
    > 
    > 如果找到一个现有表的相同的名称和架构，将追加数据，不会被覆盖。 因此，请务必删除或运行该脚本之前截断现有表。

## <a name="list-of-stored-procedures-and-functions"></a>存储的过程和函数的列表

该脚本将创建以下 SQL Server 对象：

|**SQL 脚本文件名**|**函数**|
|------|------|
|create-db-tb-upload-data.sql|创建一个数据库和两个表：<br /><br />nyctaxi_sample：包含主 NYC Taxi 数据集。 将在表中添加一个聚集列存储索引，改善存储和查询性能。 将在此表中插入 1% 的 NYC Taxi 数据集示例。<br /><br />nyc_taxi_models：用于保留已定型的高级分析模型。|
|fnCalculateDistance.sql|创建标量值函数，用于计算搭乘位置和下车位置之间直接距离|
|fnEngineerFeatures.sql|创建表值函数，用于为模型定型创建新的数据功能|
|TrainingTestingSplit.sql|将 nyctaxi_sample 表中的数据拆分为两个部分： nyctaxi_sample_training 和 nyctaxi_sample_testing。|
|PredictTipSciKitPy.sql|创建调用经过训练的模型的存储的过程 (scikit-了解) 使用该模型创建预测。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。|
|PredictTipRxPy.sql|创建调用经过训练的模型 (revoscalepy) 使用该模型创建预测的存储的过程。 该存储过程接受查询作为其输入参数，并返回包含输入行分数的数值的列。|
|PredictTipSingleModeSciKitPy.sql|创建调用经过训练的模型的存储的过程 (scikit-了解) 使用该模型创建预测。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。|
|PredictTipSingleModeRxPy.sql|创建调用经过训练的模型 (revoscalepy) 使用该模型创建预测的存储的过程。 该存储过程接受一个新观察值作为输入，而传递的单个功能值作为嵌入式参数，并返回一个预测新观察值结果的值。|

在本演练的后半部分，你将创建这些附加存储的过程：
    
|**SQL 脚本文件名**|**函数**|
|------|------|
|SerializePlots.sql|创建用于数据浏览的存储过程。 此存储的过程创建一个使用 Python 的图形，然后序列化的图形对象。|
|TrainTipPredictionModelSciKitPy.sql|创建训练逻辑回归模型的存储的过程 (scikit-了解)。 模型预测附属列的值，并使用随机选择的 60%的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|
|TrainTipPredictionModelRxPy.sql|创建训练逻辑回归模型 (revoscalepy) 的存储的过程。 模型预测附属列的值，并使用随机选择的 60%的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|

## <a name="next-step"></a>下一步

[步骤 3：浏览并可视化数据](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>上一步

[步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)

