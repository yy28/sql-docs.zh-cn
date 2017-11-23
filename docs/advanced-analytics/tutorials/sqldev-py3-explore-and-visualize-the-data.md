---
title: "步骤 3： 浏览和可视化数据 |Microsoft 文档"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-python
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 31fa666c98948dc18f7aad988de795809594d2dd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="step-3-explore-and-visualize-the-data"></a>步骤 3： 浏览和可视化数据

使用本教程，本文摘自[SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，你可以浏览示例数据并生成一些图形。 更高版本，你将了解如何在 Python 中的图形对象进行序列化然后反序列化这些对象，并进行绘图。

## <a name="review-the-data"></a>查看的数据

首先，花点时间查看浏览数据架构中，如我们所做一些更改，以更加轻松地使用 NYC Taxi 数据

+ 原始数据集用于 taxi 标识符和行程记录单独的文件。 我们已联接两个原始数据集的列上_medallion_， _hack_license_，和_pickup_datetime_。  
+ 原始数据集跨越多个文件，但很大。 我们已缩减像素采样来获取只 1%的原始的记录数。 当前数据表具有 1,703,957 行和 23 的列。

**出租车标识符**

_Medallion_列代表出租车上的唯一 ID 号。

_Hack_license_列包含 taxi 驾照号码 （匿名处理）。

**行程和费用记录**

每条行程记录都包括上车和下车地点和时间，以及行程距离。

每条费用记录都包括付费信息，如付款类型、总付款和小费金额。

最后三列可用于各种机器学习任务。  Tip_amount 列包含连续数值，并且可用作回归分析的 **label** 列。 tipped 列只有是/否值，用于二元分类。 Tip_class 列有多个**级别标签**，因此可以用作多级分类任务的标签。

用于标签列的值都基于`tip_amount`列中，使用这些业务规则：

+ 标签列`tipped`具有可能值 0 和 1

    如果`tip_amount`> 0， `tipped` = 1; 否则为`tipped`= 0

+ 标签列`tip_class`具有可能类值 0-4

    类 0: `tip_amount` = $0

    类 1: `tip_amount` > $0 和`tip_amount`< = $5
    
    类 2: `tip_amount` > $5 和`tip_amount`< = 10 美元
    
    类 3: `tip_amount` > $10 和`tip_amount`< = $20
    
    类 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>创建在 T-SQL 中使用 Python 的图形

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 由于可视化效果是此类的强大工具了解数据和离群值的分布，Python 提供很多包可视化数据。 **Matplotlib**模块是其中一个可视化效果，更受欢迎的库，包括用于创建直方图、 散点图、 框图形和其他数据浏览关系图的许多函数。

在本部分中，你将了解如何使用图形使用存储的过程。 而是不是打开服务器上的映像，你存储的 Python 对象`plot`作为**varbinary**数据，然后写入该到文件，可以是共享或其他位置查看。

### <a name="create-a-plot-as-varbinary-data"></a>创建作为 varbinary 数据绘图

**Revoscalepy** SQL Server 自 2017 年 1 机器学习服务中包含的模块支持的功能类似于**RevoScaleR**打包成。 此示例使用的 Python 等效项`rxHistogram`进行绘图时基于数据的直方图[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 

存储的过程返回的序列化的 Python`figure`对象的流作为**varbinary**数据。 不能直接查看二进制数据但你可以使用客户端上的 Python 代码来反序列化和查看的数字，然后将图像文件在客户端计算机上。

1. 创建存储的过程_SerializePlots_，如果 PowerShell 脚本未已执行此操作。

    - 变量`@query`定义查询文本`SELECT tipped FROM nyctaxi_sample`，这到 Python 代码块作为参数传递给脚本输入变量， `@input_data_1`。
    - Python 脚本是相当简单： **matplotlib** `figure`对象可用于进行使直方图和散点图，这些对象然后使用序列化`pickle`库。
    - Python 图形对象序列化为**pandas**输出的数据帧。
  
    ```SQL
    CREATE PROCEDURE [dbo].[SerializePlots]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
      EXECUTE sp_execute_external_script
      @language = N'Python',
      @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. 现在运行不带任何参数从硬编码为输入的查询的数据生成绘图的存储的过程。

    ```
    EXEC [dbo].[SerializePlots]
    ```

3. 结果应类似如下内容：
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. 从 Python 客户端，你现在可以连接到 SQL Server 实例生成的二进制绘图对象，并查看绘图。 

    若要执行此操作，运行以下 Python 代码，替换服务器名称、 数据库名称和根据需要的凭据。 请确保 Python 版本相同，则客户端和服务器上。 此外请确保在你的客户端 （例如 matplotlib) 的 Python 库的相对于服务器上安装的库的相同或更高版本。
  
    **使用 SQL Server 身份验证：**
    
    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **使用 Windows 身份验证：**

    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  如果成功连接，则你应看到如下消息：
  
    *绘图保存在目录中： xxxx*
  
6.  Python 工作目录中创建输出文件。 若要查看该绘图，找到 Python 工作目录，并打开文件。 下图显示在客户端计算机上保存绘图。
  
    ![提示量 vs 票费量](media/sqldev-python-sample-plot.png "提示量 vs 票费量") 

## <a name="next-step"></a>下一步

[步骤 4：使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一步

[步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

