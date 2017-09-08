---
title: "步骤 3：浏览和直观地显示数据 | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
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
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>步骤 3：浏览和可视化数据

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 在此步骤中，你将浏览示例数据并生成一些图形。 更高版本，您将学习如何将 Python 中的图形对象序列化为然后反序列化这些对象，并进行绘图。

> [!NOTE]
> 本演练演示了仅二元分类任务;你是欢迎尝试生成单独其他两个机器学习任务、 回归和多类分类模型。

## <a name="review-the-data"></a>查看数据

在原始数据集中，出租车标识符和行程记录在不同文件中提供。 但是，为了使示例数据易于使用，这两个原始数据集在 medallion、hack_license 和 pickup_datetime 列上进行了联接。  仅获取 1% 的原始记录作为采样记录。 所形成的低采样率数据集有 1,703,957 行和 23 列。

**出租车标识符**

- Medallion 列表示出租车的唯一 ID 号。
- Hack_license 列包含出租车司机的驾照号码（匿名）。

**行程和费用记录**

- 每条行程记录都包括上车和下车地点和时间，以及行程距离。
- 每条费用记录都包括付费信息，如付款类型、总付款和小费金额。
- 最后三列可用于各种机器学习任务。  Tip_amount 列包含连续数值，并且可用作回归分析的 **label** 列。 tipped 列只有是/否值，用于二元分类。 Tip_class 列有多个**级别标签**，因此可以用作多级分类任务的标签。
- 标签列使用的值都基于 tip_amount 列，并使用以下业务规则：
  
    |派生列名称|规则|
    |-|-|
     |tipped|如果 tip_amount > 0，则 tipped = 1；否则 tipped = 0|
    |tip_class|级别 0：tip_amount = $0<br /><br />级别 1：tip_amount > $0 且 tip_amount <= $5<br /><br />级别 2：tip_amount > $5 且 tip_amount <= $10<br /><br />级别 3：tip_amount > $10 且 tip_amount <= $20<br /><br />级别 4：tip_amount > $20|

## <a name="create-plots-using-python-in-t-sql"></a>创建在 T-SQL 中使用 Python 的图形

由于可视化效果是此类的强大工具了解数据和离群值的分布，Python 提供很多包可视化数据。 **Matplotlib**模块是一个受欢迎的库，包括用于创建直方图、 散点图、 框图形和其他数据浏览关系图的许多函数。

在本部分中，你将了解如何使用存储的过程的图形处理。 将存储`plot`Python 对象作为**varbinary**数据类型，并将保存在服务器上生成图形。

### <a name="storing-plots-as-varbinary-data-type"></a>将图表存储为 varbinary 数据类型

**Revoscalepy** SQL Server 自 2017 年 1 机器学习服务中包含的模块包含类似于 RevoScaleR 包中的 R 库的库。 在此示例中，你将使用的 Python 等效项`rxHistogram`进行绘图时基于数据的直方图[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 若要更加方便，请将包装在存储过程中，它_PlotHistogram_。

存储的过程返回的序列化的 Python`figure`对象的流作为**varbinary**数据。 不能直接查看二进制数据但你可以使用客户端上的 Python 代码来反序列化和查看的数字，然后将图像文件在客户端计算机上。

### <a name="create-the-stored-procedure-plotspython"></a>创建存储的过程 Plots_Python

1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，打开一个新**查询**窗口。

2.  选择用于本演练的数据库，并使用以下语句创建过程。 如果需要，请务必将代码修改为使用正确的表名。
  
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
**注意：**

- 变量`@query`定义查询文本 (`'SELECT tipped FROM nyctaxi_sample'`)，这到 Python 代码块作为参数传递给脚本输入变量， `@input_data_1`。
- Python 脚本是相当简单： **matplotlib** `figure`对象可用于进行使直方图和散点图，这些对象然后使用序列化`pickle`库。
- Python 图形对象序列化为 Python **pandas**输出的数据帧。

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>可查看图形文件的输出 varbinary 数据

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行以下语句：
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **结果**
  
    *绘图*
    *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...*

  
2.  在客户端计算机上运行替换服务器名称、 数据库名称和根据需要的凭据的以下 Python 代码。
  
    **SQL server 身份验证：**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **对于 Windows 身份验证：**

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

    > [!NOTE]
    > 请确保 Python 版本相同，则客户端和服务器上。 此外，请确保您在你的客户端 （例如 matplotlib) 使用的 Python 库的相对于服务器上安装的库的相同或更高版本。


3.  如果成功连接，则你将看到下面的测试结果
  
    *绘图保存在目录中： xxxx*
  
4.  将在 Python 工作目录中创建输出文件。 若要查看该绘图，只需打开 Python 工作目录。 下图显示在客户端计算机上保存示例绘图。
  
    ![提示量 vs 票费量](media/sqldev-python-sample-plot.png "提示量 vs 票费量") 

## <a name="next-step"></a>下一步

[步骤 4：使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一步

[步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)

