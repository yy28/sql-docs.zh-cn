---
title: 课 3 浏览和可视化数据使用 R 和 T-SQL （SQL Server 机器学习） |Microsoft 文档
description: 本教程演示如何将 R 嵌入在 SQL Server 中存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 057d7d988fd6f7f5d490cbf30f06e83270438983
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250080"
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>第 3 课： 浏览和可视化数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是教程的有关如何在 SQL Server 中使用 R 的 SQL 开发人员的一部分。

在本课程中，你将查看示例数据，然后生成使用某些图形[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)从[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)和泛型[Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist)函数在基的。中已包含这些 R 函数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

关键的目标演示如何调用 R 函数从[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程中并保存应用程序文件格式中的结果：

+ 创建存储的过程使用**RxHistogram**生成 varbinary 数据作为 R 绘图。 使用**bcp**将导出到图像文件的二进制流。
+ 创建存储的过程使用**Hist**生成绘图，将结果另存为 JPG 和 PDF 的输出。

> [!NOTE]
> 由于可视化效果是此类的强大工具了解数据形状和分发，R 来生成直方图、 散点图、 框图形和其他数据浏览图提供一系列的函数和包。 R 通常创建映像的 R 设备用于图形输出，你可以捕获和存储为**varbinary**在应用程序中呈现的数据类型。 此外可以将图像保存到任何支持文件格式 (。JPG、。PDF、 等）。

## <a name="review-the-data"></a>查看的数据

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 如果你尚未，所以首先花点时间查看示例数据。

在原始数据集中，出租车标识符和行程记录在不同文件中提供。 但是，若要使示例数据更易于使用，两个原始数据集尚未联接的列上_medallion_， _hack\_许可证_，和_拾取\_datetime_。  仅获取 1% 的原始记录作为采样记录。 所形成的低采样率数据集有 1,703,957 行和 23 列。

**出租车标识符**
  
-   Medallion 列表示出租车的唯一 ID 号。
  
-   _Hack\_许可证_列包含 taxi 驾照号码 （匿名处理）。
  
**行程和费用记录**
  
-   每条行程记录都包括上车和下车地点和时间，以及行程距离。
  
-   每条费用记录都包括付费信息，如付款类型、总付款和小费金额。
  
-   最后三列可用于各种机器学习任务。 _提示\_量_该列包含连续数值，并且可用作**标签**回归分析的列。 tipped 列只有是/否值，用于二元分类。 _提示\_类_列中有多个**类标签**并因此可以用作标签用于多类分类任务。
  
    本演练只演示了二元分类任务；欢迎尝试构建其他两个机器学习任务、回归和多级分类的模型。
  
-   用于标签列的值都基于_提示\_量_列中，使用这些业务规则：
  
    |派生列名称|规则|
    |-|-|
     |tipped|如果 tip_amount > 0，则 tipped = 1；否则 tipped = 0|
    |tip_class|级别 0：tip_amount = $0<br /><br />级别 1：tip_amount > $0 且 tip_amount <= $5<br /><br />级别 2：tip_amount > $5 且 tip_amount <= $10<br /><br />级别 3：tip_amount > $10 且 tip_amount <= $20<br /><br />级别 4：tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>创建存储的过程，请使用 rxHistogram 数据进行绘图时

若要创建该绘图，使用[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)中, 提供的增强的 R 函数之一[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 此步骤绘制基于数据的直方图[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。 您可以将此函数包装在存储过程中， **PlotHistogram**。

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器中，右键单击**TaxiNYC_Sample**数据库，展开**可编程性**，然后展开**存储过程**查看在第 2 课中创建的过程。

2. 右键单击**PlotHistogram**和选择**修改**要查看的源。 你可以执行此过程调用**rxHistogram**附属 nyctaxi_sample 表的列中包含的数据。

3. （可选） 作为练习，创建你自己的此存储过程，使用下面的示例副本。 打开新查询窗口并粘贴以下脚本以创建绘制直方图的存储的过程中。 此示例中名为**PlotHistogram2**以避免命名冲突使用预先存在的过程。

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram2]
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

存储的过程**PlotHistogram2**等同于预先存在的存储过程**PlotHistogram**由`RunSQL_SQL_Walkthrough.ps1`脚本。 
  
+ 变量 `@query` 定义查询文本 (`'SELECT tipped FROM nyctaxi_sample'`)，并作为脚本输入变量 `@input_data_1`的参数传递给 R 脚本。
  
+ R 脚本是相当简单： R 变量 (`image_file`) 定义存储的映像，然后**rxHistogram**函数调用以生成该绘图。
  
+ R 设备设置为**关闭**因为正在为 SQL Server 中的外部脚本运行此命令。 通常当在 R，发出高级绘图命令，R 将打开图形窗口中，调用*设备*。 可以更改窗口的大小、颜色以及其他方面，如果将输出写入文件或以其他方式处理输出，也可以关闭该设备。
  
+ R 图形序列化为 R 数据帧进行输出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>执行存储的过程并使用 bcp 将二进制数据导出到图像文件

该存储过程返回的图像是一个 varbinary 数据流，显然无法直接查看该图像。 但是，可以使用 **bcp** 实用工具获取此 varbinary 数据，并将其保存为客户端计算机上的图像文件。
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行以下语句：
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **结果**
    
    *绘图*
    *0xFFD8FFE000104A4649...*
  
2.  打开 PowerShell 命令提示符并运行以下命令，并提供适当的实例名称、 数据库名称、 用户名和凭据作为自变量。 对于那些使用 Windows 标识，可以替换 **-U**和 **-P**与 **-T**。
  
     ```text
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  TaxiNYC_Sample  -U <user name> -P <password>
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
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>创建存储的过程使用 Hist 和多个输出格式

通常情况下，数据科学家生成多个数据可视化效果来深入了解数据从不同的角度。 在此示例中，存储的过程使用 Hist 函数创建直方图，如将二进制数据导出到常用格式。JPG、。PDF、 和。PNG。 

1. 使用现有的存储的过程， **PlotInOutputFiles**、 编写直方图，scatterplots 和向其他 R 图形。JPG 和。PDF 格式。 `RunSQL_SQL_Walkthrough.ps1`创建**PlotInOutputFiles**并将其添加数据库。 使用右键单击**修改**要查看的源。

2. （可选） 作为练习，创建您自己的副本作为过程的**PlotInOutputFiles2**，具有唯一名称以避免命名冲突。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，打开一个新**查询**窗口中，并在其中粘贴以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles2]  
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
  
+ 此存储过程内的 SELECT 查询的输出存储在默认的 R 数据帧 `InputDataSet`中。 然后，可以调用各种 R 绘图函数来生成实际的图形文件。 大部分嵌入的 R 脚本表示这些图形函数的选项，如 `plot` 或 `hist`。
  
+ 所有文件保存在本地文件夹 _C:\temp\Plots\\_ 中。 此目标文件夹由作为存储过程一部分提供给 R 脚本的参数定义。  可以通过更改变量 `mainDir`的值更改此目标文件夹。

+ 若要将文件输出到另一个文件夹，请更改存储过程中嵌入的 R 脚本中 `mainDir` 变量的值。 还可以修改脚本以输出不同格式、更多文件，等等。

### <a name="execute-the-stored-procedure"></a>执行该存储过程

运行以下语句以二进制图数据导出为 JPEG 和 PDF 文件格式。

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

### <a name="view-output"></a>查看输出 

若要查看该绘图，打开目标文件夹，并查看创建的存储过程中的 R 代码的文件。

1. 请转到 STDOUT 消息中指示的文件夹 （在示例中，这是 C:\temp\plots\)

2. 打开`rHistogram_Tipped.jpg`以显示收到的提示与不收到任何提示的行程的行程次数。 （此直方图是与你在上一步中生成的一个非常类似。）

3. 打开`rHistograms_Tip_and_Fare_Amount.pdf`若要查看的提示的数量，针对票费金额绘制的分发。
    
  ![直方图显示 tip_amount 和 fare_amount](media/rsql-devtut-tipamtfareamt.PNG "直方图显示 tip_amount 和 fare_amount")

4. 打开`rXYPlots_Tip_vs_Fare_Amount.pdf`若要查看具有票费量 scatterplot 上 x 轴和 y 轴上的提示数量。

   ![提示量绘制超出票费时间](media/rsql-devtut-tipamtbyfareamt.PNG "提示量绘制超出票费时间")

## <a name="next-lesson"></a>下一课

[第 4 课： 创建使用 T-SQL 的数据功能](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一课

[第 2 课： 准备使用 PowerShell 的教程环境](../r/sqldev-import-data-to-sql-server-using-powershell.md)
