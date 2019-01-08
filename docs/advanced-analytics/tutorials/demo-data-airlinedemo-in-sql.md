---
title: 航空公司航班演示 SQL Server Python 和 R 教程-SQL Server 机器学习数据集
Description: Create a database containing the Airline dataset from R and Python. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 10d2f013c103dee3de02335ca2acf82d4320b623
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596978"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>航空公司航班到达演示数据的 SQL Server Python 和 R 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此练习中，创建一个 SQL Server 数据库来存储从 R 或 Python 内置航空公司演示数据集导入的数据。 R 和 Python 分发版提供等效的数据，可以导入到使用 Management Studio 的 SQL Server 数据库。

若要完成此练习中，您应有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或另一个工具，可运行 T-SQL 查询。

教程和快速入门使用此数据集包括：

+  [创建使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>创建数据库

1. 启动 SQL Server Management Studio，连接到数据库引擎实例具有 R 或 Python 集成。  

2. 在对象资源管理器中右键单击**数据库**并创建一个新数据库，称为**flightdata**。

3. 右键单击**flightdata**，单击**任务**，单击**导入平面文件**。

4. 打开 R 或 Python 分发，具体取决于哪种语言安装中提供的 AirlineDemoData.csv 文件。

   对于 R，寻找**AirlineDemoSmall.csv**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   对于 Python，寻找**AirlineDemoSmall.csv**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
当选中该文件时，默认值填充的表名和架构。

  ![导入平面文件向导显示航空公司演示默认值](media/import-airlinedemosmall.png)

单击完成剩余的页，接受默认设置，将数据导入。


## <a name="query-the-data"></a>查询数据

作为验证步骤，运行查询以确认数据已上传。

1. 在对象资源管理器，在数据库中右键单击**flightdata**数据库，然后启动一个新查询。

2. 运行一些简单的查询：

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>后续步骤

在下一课，您将创建基于此数据的线性回归模型。

+ [创建使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)
