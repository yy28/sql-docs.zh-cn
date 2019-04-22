---
title: 课程 1 浏览和可视化使用 Python 和 T-SQL 的 SQL Server 机器学习的数据
description: 教程演示如何嵌入 Python 在 SQL Server 存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e9dd0a0884c96a8f5b17948c21b7f891a2e997ab
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860488"
---
# <a name="explore-and-visualize-the-data"></a>浏览和可视化数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是教程的一部分[SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，将浏览示例数据并生成一些图形。 更高版本，您将了解如何在 Python 中，图形对象序列化为然后反序列化这些对象，并进行绘图。

## <a name="review-the-data"></a>查看数据

首先，花点时间来浏览数据架构，如我们所做一些更改以使其更易于使用的 NYC 出租车数据

+ 原始数据集用于出租车标识符和行程记录单独的文件。 我们已列上联接两个原始数据集_medallion_， _hack_license_，并_pickup_datetime_。  
+ 原始数据集跨越多个文件，并且非常大。 我们还进行了 downsampled 以仅获取 1%的原始记录数。 当前数据表格有 1,703,957 行和 23 列。

**出租车标识符**

_Medallion_列表示出租车的唯一 ID 号。

_Hack_license_列包含出租车司机的驾驶证编号 （匿名）。

**行程和费用记录**

每条行程记录都包括上车和下车地点和时间，以及行程距离。

每条费用记录都包括付费信息，如付款类型、总付款和小费金额。

最后三列可用于各种机器学习任务。  Tip_amount 列包含连续数值，并且可用作回归分析的 **label** 列。 tipped 列只有是/否值，用于二元分类。 Tip_class 列有多个**级别标签**，因此可以用作多级分类任务的标签。

使用标签列的值都基于`tip_amount`列中，使用以下业务规则：

+ 标签列`tipped`有可能的值 0 和 1

    如果`tip_amount`> 0， `tipped` = 1; 否则为`tipped`= 0

+ 标签列`tip_class`具有可能的类值 0 到 4

    类 0: `tip_amount` = $0

    类 1: `tip_amount` > 0 美元和`tip_amount`< = $5
    
    类 2: `tip_amount` > 5 美元和`tip_amount`< = $10
    
    类 3: `tip_amount` > 10 美元和`tip_amount`< = $20
    
    类 4: `tip_amount` > 20 美元

## <a name="create-plots-using-python-in-t-sql"></a>创建在 T-SQL 中使用 Python 的绘图

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 由于可视化是理解数据和离群值的分布用于此类的强大工具，Python 提供许多包用于可视化数据。 **Matplotlib**模块是一个用于可视化效果，更受欢迎的库，包括用于创建直方图、 散点图、 框绘图和其他数据探索图的许多函数。

在本部分中，您了解如何使用存储的过程的图形处理。 而是不是打开服务器上的映像，存储的 Python 对象`plot`作为**varbinary**数据，然后写入，到文件，可以共享，或查看其他位置。

### <a name="create-a-plot-as-varbinary-data"></a>创建绘图的形式为 varbinary 数据

存储的过程返回的序列化的 Python`figure`对象作为一串**varbinary**数据。 不能直接查看二进制数据，但可以在客户端上使用 Python 代码来反序列化并查看图形，然后保存客户端计算机上的图像文件。

1. 创建存储的过程**PyPlotMatplotlib**，如果 PowerShell 脚本未执行此操作。

    - 在变量`@query`定义的查询文本`SELECT tipped FROM nyctaxi_sample`，作为脚本输入变量的自变量传递到 Python 代码块`@input_data_1`。
    - Python 脚本是相当简单： **matplotlib** `figure`对象用于使直方图和散点图，这些对象随后会使用序列`pickle`库。
    - Python 图形对象序列化为**pandas**为输出数据帧。
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
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

2. 现在运行存储的过程不带任何参数，若要从硬编码为输入查询的数据生成绘图。

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 结果应如下所示：
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. 从[Python 客户端](../python/setup-python-client-tools-sql.md)，现在可以连接到生成的二进制绘图对象的 SQL Server 实例，并查看绘图。 

    若要执行此操作，运行以下 Python 代码中，替换服务器名称、 数据库名称和相应的凭据。 请确保 Python 版本是客户端和服务器上相同。 此外请确保在客户端 （如 matplotlib) 上的 Python 库都相对于在服务器上安装的库的相同或更高版本。
  
    **使用 SQL Server 身份验证：**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **使用 Windows 身份验证：**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  如果连接成功，应看到如下所示的消息：
  
    *绘图保存在目录中： xxxx*
  
6.  Python 工作目录中创建输出文件。 若要查看该绘图，找到 Python 工作目录，并打开该文件。 下图显示了绘图保存在客户端计算机上。
  
    ![小费金额 vs 费用金额](media/sqldev-python-sample-plot.png "小费金额 vs 费用金额") 

## <a name="next-step"></a>下一步

[使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一步

[下载 NYC 出租车数据集](demo-data-nyctaxi-in-sql.md)

