---
title: "创建关系图和使用 SQL 和 R （演练） 的图形 |Microsoft 文档"
ms.date: 11/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e720755146e8d29ddf06ccdecdd2d744c1885013
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2017
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>创建关系图和使用 SQL 和 R （演练） 的图形

在演练本部分，你了解用于生成图形和 R 使用 SQL Server 数据的地图的技术。 你创建简单的直方图，若要获取一些练习中，且无需开发更复杂的映射绘图。

### <a name="create-a-histogram"></a>创建直方图

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函数生成第一个绘图。  RxHistogram 函数提供类似于在开放源 R 包的功能，但可以在远程执行上下文中运行。

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 在开发环境的 R 图形设备中返回图像。  例如，在 RStudio 中，单击“绘图”  窗口。  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]中将打开一个单独的图形窗口。

    ![使用 rxHistogram 绘制费用金额](media/rsql-e2e-rxhistogramresult.png "使用 rxHistogram 绘制费用金额")

    > [!NOTE]
    > 图表看起来不同？
    >  
    > 这是因为_inDataSource_使用仅前 1000年行。 使用 TOP 行的顺序是不确定在 ORDER BY 子句，缺少，因此预期的数据和生成的图可能会有所不同。
    > 这一特定图像使用大约 10,000 行数据生成。 建议试验不同数量的行，获取不同的图形，并记下它在环境中返回结果所需的时间。

### <a name="create-a-map-plot"></a>创建映射绘图

通常情况下，数据库服务器阻止 Internet 访问。 使用需要下载地图或其他映像，以生成图形的 R 包时，这可能是很不方便。 但是，没有在开发自己的应用程序时你可能发现有用的解决方法。 基本上，你将生成客户端上的映射表示，然后覆盖在地图上为 SQL Server 表中的特性存储的点。

1. 定义创建 R 绘图对象的函数。 自定义函数*mapPlot*创建散点图，它使用 taxi 拾取位置，并绘制的数目会从每个位置启动。 它使用应已安装并加载的 **ggplot2** 和  **ggmap** 包。

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

    + *MapPlot*函数采用两个参数： 一个现有的数据对象，它定义以前使用 RxSqlServerData，和图表示形式传递从客户端。
    + 以开头的行中*ds*变量，rxImport 用于加载到内存数据来自之前创建的数据源*inDataSource*。 （该数据源包含仅 1000年行; 如果你想要使用更多数据点创建一个映射，你可以替换其他数据源。）
    + 无论何时使用**开源**R 函数，数据必须加载到本地内存中的数据帧。 但是，通过调用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数，你可以在运行远程计算上下文的内存。

2. 将计算上下文更改为本地，并加载创建地图所需的库。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 变量存储一组纽约时代广场的坐标。

    + 以 `googmap` 开头的行生成中心具有指定坐标的地图。

3. 切换到 SQL Server 计算上下文，并通过包装中的绘图函数来呈现结果， [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)如下所示。 RxExec 函数属于**RevoScaleR**包，并支持远程计算上下文中的任意 R 函数的执行。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中的地图数据`googMap`作为自变量传递给远程执行的函数*mapPlot*。 映射已在本地环境中生成的因为必须将它们传递给函数以便在 SQL Server 的上下文中创建该绘图。

    + 当以开头的行`plot`运行，呈现的数据将序列化回到本地的 R 环境，以便你可以在 R 客户端中查看它。

    > [!NOTE]
    > 如果使用 SQL Server 在 Azure 虚拟机，你可能在此时会出错。 这是因为在 Azure 中的默认防火墙规则阻止网络的访问权限由 R 代码。 有关如何修复此错误的详细信息，请参阅[Azure VM 中安装 R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

4. 下图显示了输出绘图。 出租车打车位置已作为红色的点添加到地图中。 你的映像可能会有所不同，具体取决于多少位置在你使用的数据源。

    ![使用自定义 R 函数绘制出租车乘坐情况](media/rsql-e2e-mapplot.png "使用自定义 R 函数绘制出租车乘坐情况")

## <a name="next-lesson"></a>下一课

[创建使用 R 和 SQL 数据功能](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>上一课

[使用 R 汇总数据](/walkthrough-view-and-summarize-data-using-r.md)
