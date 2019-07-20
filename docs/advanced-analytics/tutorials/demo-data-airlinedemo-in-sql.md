---
title: SQL Server Python 和 R 教程的航班演示数据集
Description: 从 R 和 Python 创建包含航空公司数据集的数据库。 此数据集用于演示如何在 SQL Server 存储过程中包装 R 语言或 Python 代码的练习。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 82afddf861ecda2d25260f69e532c63a1203030b
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344628"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 教程的航班到货演示数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此练习中, 将创建一个 SQL Server 数据库, 用于存储 R 或 Python 内置航空公司演示数据集的导入数据。 R 和 Python 分发版提供了等效的数据, 您可以使用 Management Studio 将其导入到 SQL Server 数据库中。

若要完成此练习, 您应该有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或可以运行 t-sql 查询的其他工具。

使用此数据集的教程和快速入门包括:

+  [使用 revoscalepy 创建 Python 模型](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>创建数据库

1. 开始 SQL Server Management Studio, 连接到具有 R 或 Python 集成的数据库引擎实例。  

2. 在对象资源管理器中, 右键单击 "**数据库**", 然后创建名为**flightdata**的新数据库。

3. 右键单击**flightdata**, 单击 "**任务**", 然后单击 "**导入平面文件**"。

4. 根据安装的语言, 打开 R 或 Python 分发版中提供的 AirlineDemoData 文件。

   对于 R, 请在 C:\Program Files\Microsoft SQL Server\MSSQL14. 中查找**airlinedemosmall.xdf。** MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   对于 Python, 请在 C:\Program Files\Microsoft SQL Server\MSSQL14. 中查找**airlinedemosmall.xdf。** MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
选择该文件时, 会为表名称和架构填写默认值。

  ![导入平面文件向导显示航空公司演示默认值](media/import-airlinedemosmall.png)

单击其余页面, 接受默认值以导入数据。


## <a name="query-the-data"></a>查询数据

作为验证步骤, 运行查询以确认已上传数据。

1. 在对象资源管理器的 "数据库" 下, 右键单击**flightdata**数据库, 然后启动一个新查询。

2. 运行一些简单的查询:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>后续步骤

在下一课中, 您将基于此数据创建线性回归模型。

+ [使用 revoscalepy 创建 Python 模型](use-python-revoscalepy-to-create-model.md)
