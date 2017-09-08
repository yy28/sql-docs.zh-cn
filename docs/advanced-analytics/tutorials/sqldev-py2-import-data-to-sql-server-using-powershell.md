---
title: "步骤 2：使用 PowerShell 将数据导入 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步骤 2：使用 PowerShell 将数据导入 SQL Server

此步骤将运行一个下载的脚本，创建演练所需的数据库对象。 该脚本还会创建大多数将使用的存储过程，并将示例数据上传到指定的数据库中的表。

## <a name="create-sql-objects-and-data"></a>创建 SQL 对象和数据

在下载的文件中，可以看到一个 PowerShell 脚本。 运行此脚本，准备用于演练的环境。  该脚本执行以下操作：

- 如果尚未安装，安装 SQL Native Client 和 SQL 命令行实用工具。 使用 **bcp**将数据大容量加载到数据库时需要这些实用程序。

- 上创建一个数据库和表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，并向表中的大容量插入数据。

- 创建多个 SQL 函数和存储的过程。

### <a name="run-the-script"></a>运行脚本

1. 以管理员身份打开 PowerShell 命令提示符并运行以下命令。
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    系统将提示输入以下信息：
    - 名称或地址[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]机器学习 Python 服务安装位置的实例
    - 实例上某帐户的用户名和密码。 使用的帐户必须能够创建数据库、创建表和存储过程，以及将数据上传到表。 如果未提供的用户名和密码，你的 Windows 标识用于登录到 SQL Server。
    - 刚下载的示例数据文件的路径和文件名。 例如，使用 IPv4 地址 `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > 请确保你 xmlrw.dll 处于你 bcp.exe 所在的文件夹。 如果没有，请通过复制它。

2.  在此步骤中，还需修改所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，以作为脚本输入提供的数据库名称和用户名替换占位符。
  
3. 花一些时间查看脚本创建的存储过程和函数。
     
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
  
4. 在本演练中的后半部分中，将创建一些附加的存储过程：
    
    |**SQL 脚本文件名**|**函数**|
    |------|------|
    |SerializePlots.sql|创建用于数据浏览的存储过程。 此存储的过程创建一个使用 Python 的图形，然后序列化的图形对象。|
    |TrainTipPredictionModelSciKitPy.sql|创建训练逻辑回归模型的存储的过程 (scikit-了解)。 模型预测附属列的值，并使用随机选择的 60%的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|
    |TrainTipPredictionModelRxPy.sql|创建训练逻辑回归模型 (revoscalepy) 的存储的过程。 模型预测附属列的值，并使用随机选择的 60%的数据进行定型。 存储过程的输出是定型模型，保存在表 nyc_taxi_models 中。|
  
3. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和指定的登录名登录到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例，验证是否可以看到创建的数据库、表、函数和存储过程。

    ![浏览在 SSMS 中的表](media/sqldev-python-browsetables1.png "在 SSMS 中查看表")

    > [!NOTE]
    > 如果数据库对象已存在，则无法再次创建。 如果表已存在，则会追加数据，而不是将其覆盖。 因此，运行脚本之前请确保删除所有现有对象。
    > 按照说明进行操作[此处](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature)以启用外部脚本服务。
    


## <a name="next-step"></a>下一步

[步骤 3：浏览和可视化数据](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>上一步

[步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)



