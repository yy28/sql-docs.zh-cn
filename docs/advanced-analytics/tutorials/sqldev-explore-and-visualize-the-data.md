---
title: 第1课使用 R 和 T-sql 浏览和可视化数据
description: 演示如何使用 R 函数浏览和可视化 SQL Server 数据的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 362e7866636f83b9c75bf75ce30a0f012b3751fa
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470639"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>第 1 课：浏览和可视化数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是有关如何在 SQL Server 中使用 R 的 SQL 开发人员教程的一部分。

在此步骤中, 你将查看示例数据, 然后使用 RevoScaleR 中的[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)和[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中的泛型[他](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist)函数生成一些图形。这些 R 函数已包含在中[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

本课的一个重要目标是演示如何从[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程中调用 R 函数, 并以应用程序文件格式保存结果:

+ 使用**RxHistogram**创建存储过程, 以将 R 绘图生成为 varbinary 数据。 使用**bcp**将二进制流导出到映像文件。
+ 使用**他**创建存储过程以生成绘图, 将结果保存为 JPG 和 PDF 输出。

> [!NOTE]
> 由于可视化效果是用于了解数据形状和分布的强大工具, 因此 R 提供了一系列函数和包, 用于生成直方图、散点图、绘图框和其他数据浏览图。 R 通常使用 R 设备创建图像以实现图形输出, 可以捕获并存储为**varbinary**数据类型, 以便在应用程序中呈现。 您还可以将图像保存到任何支持文件格式 (。JPG、。PDF 等)。

## <a name="review-the-data"></a>查看数据

开发数据科学解决方案通常包括深入的数据探索和数据可视化。 首先, 请花一分钟时间查看示例数据 (如果尚未这样做)。

在原始公共数据集中, 在单独的文件中提供出租车标识符和行程记录。 不过, 为了使示例数据更易于使用, 已将两个原始数据集加入列_medallion_、_黑客\_许可证_和 _\_分拣日期时间_。  仅获取 1% 的原始记录作为采样记录。 所形成的低采样率数据集有 1,703,957 行和 23 列。

**出租车标识符**
  
-   _Medallion_列表示出租车的唯一 id 号。
  
-   "_黑客\_许可证_" 列包含出租车驱动程序的许可证编号 (匿名)。
  
**行程和费用记录**
  
-   每条行程记录都包括上车和下车地点和时间，以及行程距离。
  
-   每条费用记录都包括付费信息，如付款类型、总付款和小费金额。
  
-   最后三列可用于各种机器学习任务。 " _Tip\_数量_" 列包含连续数值, 可用作回归分析的**标签**列。 tipped 列只有是/否值，用于二元分类。 _Tip\_class_列包含多个**类标签**, 因此可用作多类分类任务的标签。
  
    本演练只演示了二元分类任务；欢迎尝试构建其他两个机器学习任务、回归和多级分类的模型。
  
-   标签列使用的值都基于 " _tip\_数量_" 列, 使用以下业务规则:
  
    |派生列名称|规则|
    |-|-|
     |tipped|如果 tip_amount > 0，则 tipped = 1；否则 tipped = 0|
    |tip_class|级别 0：tip_amount = $0<br /><br />级别 1：tip_amount > $0 且 tip_amount <= $5<br /><br />级别 2：tip_amount > $5 且 tip_amount <= $10<br /><br />级别 3：tip_amount > $10 且 tip_amount <= $20<br /><br />级别 4：tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>使用 rxHistogram 创建存储过程以绘制数据

若要创建绘图, 请使用[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中提供的一个增强的 R 函数。 此步骤根据[!INCLUDE[tsql](../../includes/tsql-md.md)]查询中的数据绘制直方图。 可以将此函数包装在存储过程**PlotRxHistogram**中。

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的对象资源管理器中, 右键单击**NYCTaxi_Sample**数据库, 然后选择 "**新建查询**"。

2. 粘贴下面的脚本, 以创建绘制直方图的存储过程。 此示例命名为 **RPlotRxHistogram*。

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
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

在此脚本中要理解的要点包括: 
  
+ 变量 `@query` 定义查询文本 (`'SELECT tipped FROM nyctaxi_sample'`)，并作为脚本输入变量 `@input_data_1`的参数传递给 R 脚本。 对于作为外部进程运行的 R 脚本, 你应在脚本的输入之间具有一对一的映射, 并输入[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储过程, 用于在 SQL Server 上启动 R 会话。
  
+ 在 R 脚本中, 定义了一个`image_file`变量 () 来存储图像。 

+ 调用 RevoScaleR 库中的**rxHistogram**函数来生成绘图。
  
+ R 设备被设置为**off** , 因为你要在 SQL Server 中以外部脚本的形式运行此命令。 通常在 R 中, 当你发出高级绘图命令时, R 会打开一个名为 "*设备*" 的图形窗口。 如果写入文件或以其他方式处理输出, 可以关闭设备。
  
+ R 图形序列化为 R 数据帧进行输出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>执行存储过程并使用 bcp 将二进制数据导出到映像文件

该存储过程返回的图像是一个 varbinary 数据流，显然无法直接查看该图像。 但是，可以使用 **bcp** 实用工具获取此 varbinary 数据，并将其保存为客户端计算机上的图像文件。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行以下语句：
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **结果**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. 打开 PowerShell 命令提示符并运行以下命令, 并将适当的实例名称、数据库名称、用户名和凭据提供为参数。 对于使用 Windows 标识的用户, 可以将 **-U**和 **-P**替换为 **-T**。
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > Bcp 的命令开关区分大小写。
  
3. 如果连接成功，则将提示你输入有关图形文件格式的详细信息。 

   在每个提示符下按 ENTER 以接受默认设置，以下更改除外：
    
   + 对于 **prefix-length of field plot**，请键入 0
  
   + 如果想要保存输出参数供以后重复使用，则键入 **Y** 。
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **结果**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 如果将格式设置信息保存到文件 (bcp.fmt)，那么 **bcp** 实用工具将生成将来可应用于相似命令的格式定义，而不会提示输入图形文件的格式选项。 若要使用此格式文件，将 `-f bcp.fmt` 添加到任何命令行的末尾，放在 password 参数后面。
  
4.  输出文件在和运行 PowerShell 命令相同的目录中创建。 若要查看图表，只需打开文件 plot.jpg。
  
    ![带提示和不带提示的出租车行程](media/rsql-devtut-tippedornot.jpg "带提示和不带提示的出租车行程")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>使用他和多个输出格式创建存储过程

通常, 数据科学家会生成多个数据可视化, 以便从不同的角度深入分析数据。 在此示例中, 将创建一个名为**RPlotHist**的存储过程, 以将直方图、scatterplots 和其他 R 图形写入。JPG 和。PDF 格式。

此存储过程使用**他**函数创建直方图, 并将二进制数据导出为常用格式, 如。JPG、。PDF 和。PNG. 

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的对象资源管理器中, 右键单击**NYCTaxi_Sample**数据库, 然后选择 "**新建查询**"。

2. 粘贴下面的脚本, 以创建绘制直方图的存储过程。 此示例名为**RPlotHist** 。
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
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
  
+ 所有文件都保存在本地文件夹 C:\temp\Plots. 中。 此目标文件夹由作为存储过程一部分提供给 R 脚本的参数定义。  可以通过更改变量 `mainDir`的值更改此目标文件夹。

+ 若要将文件输出到另一个文件夹，请更改存储过程中嵌入的 R 脚本中 `mainDir` 变量的值。 还可以修改脚本以输出不同格式、更多文件，等等。

### <a name="execute-the-stored-procedure"></a>执行该存储过程

运行以下语句, 将二进制绘图数据导出为 JPEG 和 PDF 文件格式。

```sql
EXEC RPlotHist
```

**结果**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

文件名称中的数字是随机生成的, 以确保在尝试写入现有文件时不会出现错误。

### <a name="view-output"></a>查看输出 

若要查看绘图, 请打开目标文件夹, 并查看存储过程中由 R 代码创建的文件。

1. 前往 STDOUT 消息中所指示的文件夹 (在此示例中, 此为 C:\temp\plots\)

2. 打开`rHistogram_Tipped.jpg`此值可显示一条提示与没有提示的行程之间的行程数。 (此直方图非常类似于在上一步中生成的直方图。)

3. 打开`rHistograms_Tip_and_Fare_Amount.pdf`可查看按费用量绘制的 tip 金额的分布情况。
    
  ![显示 tip_amount 和 fare_amount 的直方图](media/rsql-devtut-tipamtfareamt.PNG "显示 tip_amount 和 fare_amount 的直方图")

4. 打开`rXYPlots_Tip_vs_Fare_Amount.pdf`此项可在 x 轴上查看具有费用量的散点图以及 y 轴上的笔尖量。

   ![费用金额绘制的 tip 量](media/rsql-devtut-tipamtbyfareamt.PNG "费用金额绘制的 tip 量")

## <a name="next-lesson"></a>下一课

[第 2 课：使用 T-sql 创建数据功能](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一课

[设置 NYC 出租车演示数据](demo-data-nyctaxi-in-sql.md)
