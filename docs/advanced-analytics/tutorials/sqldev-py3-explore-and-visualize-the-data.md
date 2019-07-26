---
title: 第1课使用 Python 和 T-sql 浏览和可视化数据
description: 介绍如何在 SQL Server 存储过程和 T-sql 函数中嵌入 Python 的教程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0442fd942f0dd509f24b98b5ca1c6d6c31a197f0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470559"
---
# <a name="explore-and-visualize-the-data"></a>浏览和可视化数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是[针对 SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)教程的一部分。 

在此步骤中, 将浏览示例数据并生成一些绘图。 稍后, 您将了解如何在 Python 中序列化图形对象, 然后对这些对象进行反序列化并制作绘图。

## <a name="review-the-data"></a>查看数据

首先, 请花点时间浏览数据架构, 因为我们做了一些更改, 以便更轻松地使用 NYC 出租车数据

+ 原始数据集对出租车标识符和行程记录使用了单独的文件。 我们已将两个原始数据集加入列_medallion_、 _hack_license_和_pickup_datetime_。  
+ 原始数据集跨多个文件, 并且非常大。 我们 downsampled 只获取原始记录数的 1%。 当前数据表包含1703957行和23列。

**出租车标识符**

_Medallion_列表示出租车的唯一 ID 号。

_Hack_license_列包含出租车驱动程序的许可证编号 (匿名)。

**行程和费用记录**

每条行程记录都包括上车和下车地点和时间，以及行程距离。

每条费用记录都包括付费信息，如付款类型、总付款和小费金额。

最后三列可用于各种机器学习任务。  Tip_amount 列包含连续数值，并且可用作回归分析的 **label** 列。 tipped 列只有是/否值，用于二元分类。 Tip_class 列有多个**级别标签**，因此可以用作多级分类任务的标签。

标签列使用的值都基于`tip_amount`列, 使用以下业务规则:

+ 标签列`tipped`的值可能为0和1

    如果`tip_amount` > 0, `tipped` = 1, 则`tipped`为; 否则为0

+ 标签列`tip_class`具有可能的类值0-4

    类 0: `tip_amount` = $0

    类 1: `tip_amount` > $0 和`tip_amount` < = $5
    
    类 2: `tip_amount` > $5 和`tip_amount` < = $10
    
    类 3: `tip_amount` > $10 和`tip_amount` < = $20
    
    类 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>在 T-sql 中使用 Python 创建绘图

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 因为可视化效果是用于了解数据和离群值分布的强大工具, 所以 Python 提供了许多用于可视化数据的包。 **Matplotlib**模块是更常用的可视化库, 其中包含许多用于创建直方图、散点图、框图和其他数据浏览图的函数。

本部分介绍如何使用存储过程来处理图形。 不要在服务器上打开该映像, 而是将 Python 对象`plot`存储为**varbinary**数据, 然后将其写入到可在其他位置共享或查看的文件。

### <a name="create-a-plot-as-varbinary-data"></a>创建绘图作为 varbinary 数据

存储过程将序列化的 Python `figure`对象作为**varbinary**数据的流返回。 您无法直接查看二进制数据, 但您可以在客户端上使用 Python 代码来反序列化和查看这些图形, 然后在客户端计算机上保存该图像文件。

1. 如果 PowerShell 脚本尚未这样做, 请创建存储过程**PyPlotMatplotlib**。

    - 变量`@query`定义查询文本, 该`SELECT tipped FROM nyctaxi_sample`文本作为脚本输入变量`@input_data_1`的参数传递到 Python 代码块。
    - Python 脚本非常简单: **matplotlib** `figure`对象用于生成直方图和散点图, `pickle`然后使用库序列化这些对象。
    - Python 图形对象被序列化到**pandas**数据帧以进行输出。
  
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

2. 现在, 请运行不带参数的存储过程, 以生成从硬编码为输入查询的数据的绘图。

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

  
4. 你现在可以从[Python 客户端](../python/setup-python-client-tools-sql.md)连接到生成了二进制绘图对象的 SQL Server 实例, 并查看图形。 

    为此, 请运行以下 Python 代码, 并根据需要替换服务器名称、数据库名称和凭据。 请确保在客户端和服务器上的 Python 版本相同。 此外, 请确保客户端上的 Python 库 (如 matplotlib) 与服务器上安装的库的版本相同或更高。
  
    **使用 SQL Server 身份验证:**
    
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

    **使用 Windows 身份验证:**

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

5.  如果连接成功, 应会看到如下所示的消息:
  
    *绘图将保存在目录中: xxxx*
  
6.  在 Python 工作目录中创建输出文件。 若要查看绘图, 请找到 Python 工作目录, 并打开文件。 下图显示了在客户端计算机上保存的绘图。
  
    ![Tip 金额与费用金额](media/sqldev-python-sample-plot.png "Tip 金额与费用金额") 

## <a name="next-step"></a>下一步

[使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一步

[下载 NYC 出租车数据集](demo-data-nyctaxi-in-sql.md)

