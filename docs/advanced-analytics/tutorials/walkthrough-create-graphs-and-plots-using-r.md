---
title: 使用 SQL 和 R 函数创建图形和绘图-SQL Server 机器学习
description: 介绍如何在 SQL Server 上使用 R 语言函数创建图形和绘图的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f14005b8ba9d6f05d2b69deba29d83af5695f657
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470502"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>使用 SQL 和 R 创建图形和绘图 (演练)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本演练的此部分中, 你将学习使用 R 和 SQL Server 数据生成图形和地图的方法。 创建一个简单的直方图, 然后开发更复杂的地图绘图。

## <a name="prerequisites"></a>先决条件

此步骤假设正在进行的 R 会话基于本演练中前面的步骤。 它使用在这些步骤中创建的连接字符串和数据源对象。 以下工具和包用于运行脚本。

+ Rgui.exe 运行 R 命令
+ Management Studio 运行 T-sql
+ googMap
+ ggmap 包
+ mapproj 包

## <a name="create-a-histogram"></a>创建直方图

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函数生成第一个绘图。  RxHistogram 函数提供的功能类似于开放源代码 R 包中的功能, 但可在远程执行上下文中运行。

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
    > 图形外观是否不同？
    >  
    > 这是因为, _inDataSource_只使用前1000行。 如果没有 ORDER BY 子句, 则使用 TOP 的行的顺序是不确定的, 因此, 数据和生成的关系图可能会有所不同。
    > 这一特定图像使用大约 10,000 行数据生成。 建议试验不同数量的行，获取不同的图形，并记下它在环境中返回结果所需的时间。

## <a name="create-a-map-plot"></a>创建地图绘图

通常, 数据库服务器阻止 Internet 访问。 使用需要下载地图或其他图像以生成图形的 R 包时, 这会很不方便。 但是, 在开发自己的应用程序时可能会发现很有用的一种解决方法。 基本上, 你将在客户端上生成地图表示形式, 然后在地图上叠加存储为 SQL Server 表中的属性的点。

1. 定义用于创建 R 绘图对象的函数。 自定义函数*mapPlot*创建一个使用出租车拾取位置的散点图, 并绘制从每个位置开始的搭乘数量。 它使用应已[安装并加载](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)的**ggplot2**和**ggmap**包。

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

    + *MapPlot*函数采用两个参数: 之前使用 RxSqlServerData 定义的现有数据对象, 以及从客户端传递的地图表示形式。
    + 在以*ds*变量开头的行中, 使用 rxImport 从以前创建的数据源*inDataSource*加载到内存数据。 (该数据源仅包含1000行; 如果要创建具有更多数据点的地图, 则可以使用不同的数据源。)
    + 无论何时使用开源 R 函数, 都必须将数据加载到本地内存中的数据帧。 但是, 通过调用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数, 你可以在远程计算上下文的内存中运行。

2. 将计算上下文更改为 "本地", 并加载创建映射所需的库。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 变量存储一组纽约时代广场的坐标。

    + 以 `googmap` 开头的行生成中心具有指定坐标的地图。

3. 切换到 SQL Server 计算上下文, 并通过将绘图函数包装在[rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)中 (如下所示) 来呈现结果。 RxExec 函数是**RevoScaleR**包的一部分, 它支持在远程计算上下文中执行任意 R 函数。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中`googMap`的映射数据作为参数传递到远程执行的函数*mapPlot*。 因为映射是在本地环境中生成的, 所以必须将其传递到函数, 以便在 SQL Server 的上下文中创建绘图。

    + 当行以`plot`开头运行时, 呈现的数据将被序列化为本地 R 环境, 以便可以在 R 客户端中查看它。

    > [!NOTE]
    > 如果在 Azure 虚拟机中使用 SQL Server, 则此时可能会出现错误。 如果 Azure 中的默认防火墙规则阻止 R 代码进行网络访问, 则会发生错误。 有关如何解决此错误的详细信息, 请参阅[在 AZURE VM 上安装机器学习 (R) 服务](../install/sql-machine-learning-azure-virtual-machine.md)。

4. 下图显示了输出绘图。 出租车打车位置已作为红色的点添加到地图中。 根据你使用的数据源中有多少个位置, 你的映像可能会有所不同。

    ![使用自定义 R 函数绘制出租车乘坐情况](media/rsql-e2e-mapplot.png "使用自定义 R 函数绘制出租车乘坐情况")

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 和 SQL 创建数据功能](walkthrough-create-data-features.md)
