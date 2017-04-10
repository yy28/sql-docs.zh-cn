---
title: "使用 R 创建图形和绘图（数据科学端到端演练） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 创建图形和绘图（数据科学端到端演练）
在本课程中，将学习搭配使用 R 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据生成绘图和映射的技巧。  可见，查看在服务器上创建的绘图是多么容易，并可以了解如何将图形对象传递到服务器。  
  
## <a name="creating-graphics"></a>创建图形
在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，图形对象、模型和结果会在计算机和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算上下文之间序列化。

使用 SQL Server 计算上下文时，可能无法下载地图表示形式，因为大多数生产服务器会完全阻止 Internet 访问。  因此，若要创建第二组绘图，需在客户端生成地图表示形式，然后在地图上覆盖作为属性存储在 nyctaxi_sample 表中的点。   

为此，首先通过调用 Google 地图创建地图表示法，然后将地图表示形式传递到 SQL 上下文。  
  
在开发自己的应用程序时，可能会发现这种模式非常有用。   
  
### <a name="create-a-histogram"></a>创建直方图  
若要创建直方图，可将先前创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源与 R Services 中提供的 `rxHistogram` 函数搭配使用。  
  
1.  使用 rxHistogram 函数生成第一个绘图。  rxHistogram 函数提供的功能类似于开放源代码 R 包的功能，但可在远程执行上下文中运行。 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  在开发环境的 R 图形设备中返回图像。  例如，在 RStudio 中，单击“绘图”窗口。  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]中将打开一个单独的图形窗口。  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  由于没有 ORDER BY 子句，无法确定使用 TOP 的行的顺序，因此可能会看到截然不同的结果。 建议试验不同数量的行，获取不同的图形，并记下它在环境中返回结果所需的时间。  这一特定图像使用 ~10,000 行数据生成。
  
### <a name="create-a-map-plot"></a>创建地图绘图  
在此示例中，将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例作为计算上下文生成绘图对象，然后将绘图对象返回本地计算上下文进行呈现。  
   
1.  首先，定义创建绘图对象的函数。  

    ```R  
    mapPlot <- function(inDataSource, googMap){  
        library(ggmap)  
        library(mapproj)     
        ds <- rxImport(inDataSource)  
        p <- ggmap(googMap)+  
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,  
    color="darkred", size = 1.5)  
        return(list(myplot=p))  
    }  
    ```  
    + 自定义 R 函数 mapPlot 会创建一个散点图，该散点图使用出租车接客位置绘制从每个位置开始的搭乘数。 它使用应已安装并加载的 **ggplot2** 和  **ggmap** 包。  
    + mapPlot 函数采用两个参数：之前使用 RxSqlServerData定义的现有数据对象，以及从客户端传递的地图表示形式。    
    + 请注意，使用 ds 变量从先前创建的数据源 inDataSource 加载数据。  只要使用开放源代码 R 函数，就必须将数据加载到内存中的数据帧。 可以通过使用 RevoScaleR 包中的 rxImport 函数实现此操作。  但是，此函数在之前定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上下文的内存中运行。 也就是说，该函数不使用本地工作站的内存。  
  
2.  接下来，加载在本地 R 环境中创建地图所需的库。  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + 此代码在 R 客户端上运行。 请注意对 **ggmap** 和 **mapproj**库的重复调用。 原因是上一个函数定义在服务器上下文中运行，且从未本地加载这些库；而现在要将绘图操作返回到工作站。  
  
    -   gc 变量存储一组纽约时代广场的坐标。  
  
    -   以 googmap 开头的行生成中心具有指定坐标的地图。  
          
  
3.  执行绘图函数，并呈现本地 R 环境中的结果。 为此，将绘图函数包含到 rxExec 中，如此处所示。  rxExec  函数包含在 RevoScaleR 包中，并支持在远程计算上下文中执行任意 R 函数。 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + 在第一行中，可以看到地图数据作为参数 (googMap) 传递到远程执行的函数 mapPlot 中。 这是因为这些地图是在本地环境中生成的，且必须将其传递到函数，以便在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上下文中创建绘图。   
  
        然后，将呈现的数据序列化回本地 R 环境，以便可以使用 RStudio 或其他 R 图形设备中的“绘图”窗口进行查看。  
  
  
4.  下面是输出绘图，以红色的点显示地图上的接客位置。  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>下一课  
[第 3 课：创建数据功能（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
