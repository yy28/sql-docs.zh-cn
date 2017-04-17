---
title: "步骤 3：浏览和直观地显示数据 | Microsoft Docs"
ms.custom: 
ms.date: 04/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: de6008e773d6f895cad475798e05a02ae2411b41
ms.lasthandoff: 04/11/2017

---
# <a name="step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial"></a>步骤 3：浏览和可视化数据（数据库内高级分析教程）
开发数据科学解决方案通常包括深入的数据探索和数据可视化。 在此步骤中，将查看示例数据，并使用 R 函数生成一些图形。 这些 R 函数已包括在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中；在本演练中，将练习从 [!INCLUDE[tsql](../../includes/tsql-md.md)]调用 R 函数。  
  
## <a name="review-the-data"></a>查看数据  
首先，花点时间查看示例数据（如果尚未查看）。  
  
在原始数据集中，出租车标识符和行程记录在不同文件中提供。 但是，为了使示例数据易于使用，这两个原始数据集在 medallion、hack_license 和 pickup_datetime 列上进行了联接。  仅获取 1% 的原始记录作为采样记录。 所形成的低采样率数据集有 1,703,957 行和 23 列。  
  
**出租车标识符**  
  
-   Medallion 列表示出租车的唯一 ID 号。  
  
-   Hack_license 列包含出租车司机的驾照号码（匿名）。  
  
**行程和费用记录**  
  
-   每条行程记录都包括上车和下车地点和时间，以及行程距离。  
  
-   每条费用记录都包括付费信息，如付款类型、总付款和小费金额。  
  
-   最后三列可用于各种机器学习任务。  Tip_amount 列包含连续数值，并且可用作回归分析的 **label** 列。 tipped 列只有是/否值，用于二元分类。 Tip_class 列有多个**级别标签**，因此可以用作多级分类任务的标签。  
  
    本演练只演示了二元分类任务；欢迎尝试构建其他两个机器学习任务、回归和多级分类的模型。  
  
-   标签列使用的值都基于 tip_amount 列，并使用以下业务规则：  
  
    |派生列名称|规则|  
    |-|-|  
     |tipped|如果 tip_amount > 0，则 tipped = 1；否则 tipped = 0|  
    |tip_class|级别 0：tip_amount = $0<br /><br />级别 1：tip_amount > $0 且 tip_amount <= $5<br /><br />级别 2：tip_amount > $5 且 tip_amount <= $10<br /><br />级别 3：tip_amount > $10 且 tip_amount <= $20<br /><br />级别 4：tip_amount > $20|  
  
## <a name="create-plots-using-r-in-t-sql"></a>使用 T-SQL 中的 R 创建图表  
由于可视化是理解数据和离群值的分布的强大工具，因此 R 提供了许多用于可视化数据的包。 R 的标准开源分发版还包括用于创建直方图、散点图、箱形图和其他数据探索图的许多函数。  
  
R 通常使用用于图形输出的 R 设备创建图像。 可以捕获此设备的输出，并将图像存储为 **varbinary** 数据类型，以便在应用程序中呈现，也可以将图像保存为任何支持的文件格式（.JPG、.PDF 等）。  
  
在本部分中，将了解如何使用存储过程处理每种类型的输出。  
  
-   将图表存储为 varbinary 数据类型  
  
-   将图表保存在服务器的文件（.JPG、.PDF）中  
  
### <a name="storing-plots-as-varbinary-data-type"></a>将图表存储为 varbinary 数据类型  
使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中提供的一个增强型 R 函数 `rxHistogram`，根据 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询的数据绘制直方图。 若要更加轻松地调用 R 函数，请将其包装在存储过程 PlotHistogram 中。  
  
该存储过程返回的图像是一个 varbinary 数据流，显然无法直接查看该图像。 但是，可以使用 **bcp** 实用工具获取此 varbinary 数据，并将其保存为客户端计算机上的图像文件。  
  
##### <a name="to-create-the-stored-procedure-plothistogram"></a>创建存储过程 PlotHistogram  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开一个新的查询窗口。  
  
2.  选择用于本演练的数据库，并使用以下语句创建过程。  
  
    ```  
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
  
    -   R 图形序列化为 R 数据帧进行输出。 这是针对 CTP3 的临时解决办法。  
  
##### <a name="to-output-varbinary-data-to-viewable-graphics-file"></a>将 varbinary 数据输出为可查看的图形文件  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，运行以下语句：  
  
    ```  
    EXEC [dbo].[PlotHistogram]  
    ```  
  
**结果**  
  
*plot*  
*0xFFD8FFE000104A4649...*  
  
2.  打开 PowerShell 命令提示符，并运行以下命令，提供相应的作为参数的实例名称、数据库名称、用户名和凭据：  
  
    ```  
    bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>  
  
    ```  
  
    > [!NOTE]  
    > **bcp** 的命令开关区分大小写。  
  
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
  
*Starting copy...*  
*1 rows copied.*  
*Network packet size (bytes): 4096*  
*时钟时间(毫秒)总计值     : 3922   平均值 : (每秒 0.25 行。)*  
   
> [!TIP]  
 > 如果将格式设置信息保存到文件 (bcp.fmt)，那么 **bcp** 实用工具将生成将来可应用于相似命令的格式定义，而不会提示输入图形文件的格式选项。 若要使用此格式文件，将 `-f bcp.fmt` 添加到任何命令行的末尾，放在 password 参数后面。  
  
4.  输出文件在和运行 PowerShell 命令相同的目录中创建。 若要查看图表，只需打开文件 plot.jpg。  
  
    ![带提示和不带提示的出租车行程](../../advanced-analytics/r-services/media/rsql-devtut-tippedornot.jpg "带提示和不带提示的出租车行程")  
  
### <a name="saving-plots-in-files-jpg-pdf-on-the-server"></a>将图表保存在服务器的文件（jpg、pdf）中  
将 R 图表输出为二进制数据类型可能便于应用程序使用，但是对于需要在数据探索阶段呈现图表的数据科学家来说并不十分有用。 通常数据科学家生成多个数据可视化，以便从不同的角度深入了解数据。  
  
若要生成可以更轻松地查看的图形，可以使用存储过程创建常用格式的 R 输出，例如 .JPG、.PDF 和 .PNG。 存储过程创建图形后，只需打开文件即可显示图表。  
  
在此步骤中，将创建新的存储过程 PlotInOutputFiles，演示如何使用 R 绘图函数来创建 .JPG 和 .PDF 格式的直方图、散点图以及其他图。 图形文件保存到本地文件；即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的文件夹中。  
  
##### <a name="to-create-the-stored-procedure-plotinoutputfiles"></a>创建存储过程 PlotInOutputFiles  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开一个新的查询窗口，在其中粘贴以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
    ```  
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
  
    -   所有文件保存在本地文件夹 _C:\temp\Plots\\_ 中。  
  
        此目标文件夹由作为存储过程一部分提供给 R 脚本的参数定义。  可以通过更改变量 `mainDir`的值更改此目标文件夹。  
  
2.  运行该语句以创建存储过程。  
  
  
##### <a name="to-generate-the-graphics-files"></a>生成图形文件  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，运行以下 SQL 查询：  
  
    ```  
    EXEC PlotInOutputFiles  
  
    ```  
  
**结果**  
  
*STDOUT message(s) from external script:*  
*[1] Creating output plot files:[1]* *C:\\\temp\\\plots\\\rHistogram_Tipped_18887f6265d4.jpg[1]* *C:\\\temp\\\plots\\\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]* *C:\\\temp\\\plots\\\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf*  
  
2.  打开目标文件夹，并查看存储过程中 R 代码创建的文件。 （文件名中的数字是随机生成的。）  
  
*  rHistogram_Tipped_*nnnn*.jpg：显示得到小费的行程数量 (1) 和未得到小费的行程数量 (0) 的比较。 此直方图与上一步中生成的直方图非常相似。  
  
*  rHistograms_Tip_and_Fare_Amount_*nnnn*.pdf：显示 tip_amount 和 fare_amount 列中值的分布情况。  
  
        ![histogram showing tip_amount and fare_amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtfareamt.PNG "histogram showing tip_amount and fare_amount")  
  
*  rXYPlots_Tip_vs_Fare_Amount_*nnnn*.pdf：一个散点图，x 轴为费用金额，y 轴为小费金额。  
  
        ![tip amount plotted over fare amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtbyfareamt.PNG "tip amount plotted over fare amount")  
  
3.  若要将文件输出到另一个文件夹，请更改存储过程中嵌入的 R 脚本中 `mainDir` 变量的值。  
  
    还可以修改脚本以输出不同格式、更多文件，等等。  
  
## <a name="next-step"></a>下一步  
[步骤 4：使用 T-SQL 创建数据功能](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## <a name="previous-step"></a>上一步  
[步骤 2：使用 PowerShell 将数据导入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  


