---
title: 使用 SQL 和 R 函数的 SQL Server 机器学习创建图形和绘图
description: 本教程演示如何在 SQL Server 上使用 R 语言函数创建图形和绘图。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 542e36e01565ab454cce8beae9a4fa65279d8fa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961785"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>使用 SQL 和 R （演练） 创建图形和绘图
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本演练的此部分中，了解用于生成绘图和映射具有 SQL Server 数据使用 R 的技术。 创建简单的直方图，然后开发更复杂的地图绘图。

## <a name="prerequisites"></a>系统必备

此步骤假定正在进行 R 会话基于本演练中之前的步骤。 它使用这些步骤中创建的连接字符串和数据源对象。 使用以下工具和包来运行脚本。

+ 若要运行 R 命令的 Rgui.exe
+ Management Studio 来运行 T-SQL
+ googMap
+ ggmap 包
+ mapproj 包

## <a name="create-a-histogram"></a>创建直方图

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函数生成第一个绘图。  RxHistogram 函数提供的功能类似于在开放源代码 R 包，但可以在远程执行上下文中运行。

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
    > 图形看上去不同？
    >  
    > 这是因为_inDataSource_使用只显示前 1000年行。 使用 TOP 的行排序是在没有 ORDER BY 子句，非确定性的因此预期的数据和生成的关系图可能会有所不同。
    > 这一特定图像使用大约 10,000 行数据生成。 建议试验不同数量的行，获取不同的图形，并记下它在环境中返回结果所需的时间。

## <a name="create-a-map-plot"></a>创建地图绘图

通常情况下，数据库服务器会阻止 Internet 访问权限。 使用 R 包，需要下载映射或其他图像以生成图形时，这可能很不方便。 但是，没有解决方法是，开发自己的应用程序时您可能会有帮助。 基本上，您生成在客户端上的地图表示形式，然后在地图上覆盖作为属性在 SQL Server 表中存储的点。

1. 定义创建 R 绘图对象的函数。 自定义函数*mapPlot*创建散点图使用出租车接客位置，并绘制从每个位置开始的搭乘数。 它使用**ggplot2**并**ggmap**包，应[安装并加载](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)。

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

    + *MapPlot*函数采用两个参数： 一个现有的数据对象，它定义之前使用 RxSqlServerData，并从客户端传递的地图表示形式。
    + 在开头的行*ds*变量，rxImport 用于将加载到内存数据从先前创建的数据源*inDataSource*。 （该数据源包含仅 1000年行; 如果你想要使用更多数据点创建地图，您可以替换不同的数据源。）
    + 只要使用开放源代码 R 函数，则必须将数据加载到本地内存中的数据帧。 但是，通过调用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数，您可以运行在远程计算上下文的内存中。

2. 将计算上下文更改为本地，并加载用于创建地图所需的库。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 变量存储一组纽约时代广场的坐标。

    + 以 `googmap` 开头的行生成中心具有指定坐标的地图。

3. 切换到 SQL Server 计算上下文，并通过包装中的绘图函数来呈现结果[rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)如下所示。 RxExec 函数属于**RevoScaleR**包，并支持执行任意 R 函数，在远程计算上下文中。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中的地图数据`googMap`作为参数传递给远程执行的函数*mapPlot*。 由于映射在本地环境中生成的它们必须以 SQL Server 的上下文中创建绘图传递给函数。

    + 当开头的行`plot`运行时，呈现的数据序列化回复到本地 R 环境，以便您可以在 R 客户端中查看它。

    > [!NOTE]
    > 如果 Azure 虚拟机中使用 SQL Server，可能在此时会遇到错误。 在 Azure 中的默认防火墙规则阻止网络访问权限由 R 代码时，就会出错。 有关如何修复此错误的详细信息，请参阅[Azure VM 上安装机器学习 （R) Services](../install/sql-machine-learning-azure-virtual-machine.md)。

4. 下图显示了输出绘图。 出租车打车位置已作为红色的点添加到地图中。 您的图像看起来会有所不同，具体取决于多少个位置在您使用的数据源中。

    ![使用自定义 R 函数绘制出租车乘坐情况](media/rsql-e2e-mapplot.png "使用自定义 R 函数绘制出租车乘坐情况")

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 和 SQL 创建数据功能](walkthrough-create-data-features.md)
