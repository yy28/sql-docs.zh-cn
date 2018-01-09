---
title: "第 3 课： 浏览和可视化数据 |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8048bc1eff7437e2a96bd8995f0362b341cbf092
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>第 3 课： 浏览和可视化数据

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

在本课程中，你将查看示例数据，然后生成使用 R 函数某些图形。 中已包含这些 R 函数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 你可以调用中的 R 函数[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="review-the-data"></a>查看的数据

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 如果你尚未，所以首先花点时间查看示例数据。

在原始数据集中，出租车标识符和行程记录在不同文件中提供。 但是，若要使示例数据更易于使用，两个原始数据集尚未联接的列上_medallion_， _hack\_许可证_，和_拾取\_datetime_。  仅获取 1% 的原始记录作为采样记录。 所形成的低采样率数据集有 1,703,957 行和 23 列。

**出租车标识符**
  
-   Medallion 列表示出租车的唯一 ID 号。
  
-   _Hack\_许可证_列包含 taxi 驾照号码 （匿名处理）。
  
**行程和费用记录**
  
-   每条行程记录都包括上车和下车地点和时间，以及行程距离。
  
-   每条费用记录都包括付费信息，如付款类型、总付款和小费金额。
  
-   最后三列可用于各种机器学习任务。  _提示\_量_该列包含连续数值，并且可用作**标签**回归分析的列。 tipped 列只有是/否值，用于二元分类。 _提示\_类_列中有多个**类标签**并因此可以用作标签用于多类分类任务。
  
    本演练只演示了二元分类任务；欢迎尝试构建其他两个机器学习任务、回归和多级分类的模型。
  
-   用于标签列的值都基于_提示\_量_列中，使用这些业务规则：
  
    |派生列名称|规则|
    |-|-|
     |tipped|如果 tip_amount > 0，则 tipped = 1；否则 tipped = 0|
    |tip_class|级别 0：tip_amount = $0<br /><br />级别 1：tip_amount > $0 且 tip_amount <= $5<br /><br />级别 2：tip_amount > $5 且 tip_amount <= $10<br /><br />级别 3：tip_amount > $10 且 tip_amount <= $20<br /><br />级别 4：tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>创建在 T-SQL 中使用 R 的图形

由于可视化是理解数据和离群值的分布的强大工具，因此 R 提供了许多用于可视化数据的包。 R 的标准开源分发版还包括用于创建直方图、散点图、箱形图和其他数据探索图的许多函数。

R 通常使用用于图形输出的 R 设备创建图像。 可以捕获此设备的输出，并将图像存储为 **varbinary** 数据类型，以便在应用程序中呈现，也可以将图像保存为任何支持的文件格式（.JPG、.PDF 等）。

在本部分中，将了解如何使用存储过程处理每种类型的输出。 整个过程是，如下所示：

- 创建存储的过程生成 varbinary 数据作为 R 绘图

- 生成该绘图，并将其保存到图像文件

- 使用存储的过程将二进制绘图数据转换为的 JPG 或 PDF 文件

### <a name="create-the-stored-procedure-plothistogram"></a>创建存储的过程 PlotHistogram

1. 若要创建该绘图，使用`rxHistogram`中, 提供的增强的 R 函数之一[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]、 要绘制基于数据的直方图[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 若要更加轻松地调用 R 函数，请将其包装在存储过程 PlotHistogram 中。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，打开一个新**查询**窗口。

2. 在数据库中包含的教程数据，创建使用此语句的过程：

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

    如果需要，请务必将代码修改为使用正确的表名。
  
    -   变量 `@query` 定义查询文本 (`'SELECT tipped FROM nyctaxi_sample'`)，并作为脚本输入变量 `@input_data_1`的参数传递给 R 脚本。
  
    -   R 脚本非常简单：定义 R 变量 (`image_file`) 用于存储图像，然后调用 `rxHistogram` 函数生成图表。
  
    -   R 设备设置为“关闭”。
  
        在 R 中，当发出高级绘图命令时，R 将打开一个图形窗口，该窗口称为“设备”。 可以更改窗口的大小、颜色以及其他方面，如果将输出写入文件或以其他方式处理输出，也可以关闭该设备。
  
    -   R 图形序列化为 R 数据帧进行输出。

### <a name="generate-the-graphics-data-and-save-to-file"></a>生成图形数据，并将保存到文件

该存储过程返回的图像是一个 varbinary 数据流，显然无法直接查看该图像。 但是，可以使用 **bcp** 实用工具获取此 varbinary 数据，并将其保存为客户端计算机上的图像文件。
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行以下语句：
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **结果**
    
    *绘图*
    *0xFFD8FFE000104A4649...*
  
2.  打开 PowerShell 命令提示符，并运行以下命令，提供相应的作为参数的实例名称、数据库名称、用户名和凭据：
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Bcp 的命令开关是区分大小写。
  
3.  如果连接成功，则将提示你输入有关图形文件格式的详细信息。 在每个提示符下按 ENTER 以接受默认设置，以下更改除外：
  
    -   对于 **prefix-length of field plot**，请键入 0
  
    -   如果想要保存输出参数供以后重复使用，则键入 **Y** 。
  
    ```
    Enter the file storage type of field plot [varbinary(max)]:
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **结果**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 如果将格式设置信息保存到文件 (bcp.fmt)，那么 **bcp** 实用工具将生成将来可应用于相似命令的格式定义，而不会提示输入图形文件的格式选项。 若要使用此格式文件，将 `-f bcp.fmt` 添加到任何命令行的末尾，放在 password 参数后面。
  
4.  输出文件在和运行 PowerShell 命令相同的目录中创建。 若要查看图表，只需打开文件 plot.jpg。
  
    ![带提示和不带提示的出租车行程](media/rsql-devtut-tippedornot.jpg "带提示和不带提示的出租车行程")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>将图形数据导出到可查看文件

输出 R 绘图的二进制数据类型可能会供应用程序，使用方便，但它不是为数据科学家需要呈现的绘图的数据浏览阶段非常有用。 通常数据科学家生成多个数据可视化，以便从不同的角度深入了解数据。

若要生成的用户的关系图，可以使用创建的 R 输出中常用的格式，如存储的过程。JPG、。PDF、 和。PNG。 存储过程创建图形后，只需打开文件即可显示图表。

1. 创建一个新的存储的过程， _PlotInOutputFiles_，演示如何编写直方图、 scatterplots 和向其他 R 图形。JPG 和。PDF 格式。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，打开一个新**查询**窗口中，并在其中粘贴以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
    -   此存储过程内的 SELECT 查询的输出存储在默认的 R 数据帧 `InputDataSet`中。 然后，可以调用各种 R 绘图函数来生成实际的图形文件。
  
        大部分嵌入的 R 脚本表示这些图形函数的选项，如 `plot` 或 `hist`。
  
    -   所有文件保存在本地文件夹 _C:\temp\Plots\\_ 中。 此目标文件夹由作为存储过程一部分提供给 R 脚本的参数定义。  可以通过更改变量 `mainDir`的值更改此目标文件夹。
  
2.  运行该语句以创建存储过程。

    ```SQL
    EXEC PlotInOutputFiles
    ```

    **结果**
    
    ```
    STDOUT message(s) from external script:
    [1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 
    
    C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]
    
    C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
    ```

    随机生成的文件名称中的数字以确保在尝试写入到现有文件时不会出错。

3. 若要查看该绘图，打开目标文件夹，并查看创建的存储过程中的 R 代码的文件。

    + 文件`rHistogram_Tipped.jpg`显示了与不收到任何提示的行程的提示的行程次数。 （此直方图是与你在上一步中生成的一个非常类似。）

    + 文件`rHistograms_Tip_and_Fare_Amount.pdf`显示提示的数量，针对票费金额绘制的分布。
    
    ![直方图显示 tip_amount 和 fare_amount](media/rsql-devtut-tipamtfareamt.PNG "直方图显示 tip_amount 和 fare_amount")

    + 文件`rXYPlots_Tip_vs_Fare_Amount.pdf`包含与票费量 x 轴和 y 轴上的提示量 scatterplot。

    ![提示量绘制超出票费时间](media/rsql-devtut-tipamtbyfareamt.PNG "提示量绘制超出票费时间")

2.  若要将文件输出到另一个文件夹，请更改存储过程中嵌入的 R 脚本中 `mainDir` 变量的值。 还可以修改脚本以输出不同格式、更多文件，等等。

## <a name="next-lesson"></a>下一课

[第 4 课： 创建使用 T-SQL 的数据功能](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一课

[第 2 课： 将数据导入到 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)
