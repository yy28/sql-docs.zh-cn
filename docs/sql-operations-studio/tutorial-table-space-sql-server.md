---
title: "教程： 启用表空间使用情况示例见解小组件，在 SQL 操作 Studio （预览版） |Microsoft 文档"
description: "本教程演示如何启用表空间使用情况示例见解小组件，在 SQL 操作 Studio （预览版） 数据库仪表板。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c51c7d1804baa490e665d316a08d911038c9f11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教程： 启用表空间使用使用情况示例见解小组件[!INCLUDE[name-sos](../includes/name-sos-short.md)]

本教程演示如何启用数据库中的所有表中提供的空间使用情况有关的一览式视图的数据库仪表板见解小组件。 在本教程中，你学习如何：

> [!div class="checklist"]
> * 快速开启使用内置的见解小组件示例见解小组件
> * 查看表空间使用情况的详细信息
> * 筛选数据，并在见解图表上查看标签的详细信息

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>开启的管理见解[!INCLUDE[name-sos](../includes/name-sos-short.md)]的数据库仪表板
[!INCLUDE[name-sos](../includes/name-sos-short.md)]具有内置示例小组件监视数据库的表中所用的空间。

1. 打开**用户设置**按**Ctrl + Shift + P**以打开*命令控制板*，类型*设置*在搜索框中，选择**首选项： 打开用户设置**。

   ![打开用户设置命令](./media/tutorial-table-space-sql-server/open-user-settings.png)

2. 类型*仪表板*中设置搜索输入框中，找到**dashboard.database.widgets**。

   ![搜索设置](./media/tutorial-table-space-sql-server/search-settings.png)

3. 若要自定义**dashboard.database.widgets**设置，将鼠标悬停在左侧的铅笔图标**dashboard.database.widgets**文本，单击**编辑** > **复制到设置**。

4. 使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的见解设置 IntelliSense，配置*名称*小组件标题*gridItemConfig*对于小组件大小，和*小组件*通过选择**表空间 db 见解**从下拉列表，如下面的屏幕截图中所示：

   ![见解设置](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 按**Ctrl + S**以保存设置。

6. 通过右键单击打开的数据库仪表板**TutorialDB**单击**管理**。

   ![打开仪表板](./media/tutorial-table-space-sql-server/insight-open-dashboard.png)

7. 视图*使用的表空间*下面的屏幕截图中所示： 

   ![小组件](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>使用见解图表

[!INCLUDE[name-sos](../includes/name-sos-short.md)]见解图表提供筛选和鼠标悬停时的详细信息。 若要尝试以下步骤：

1. 单击并切换*row_count*图表上的图例。 [!INCLUDE[name-sos](../includes/name-sos-short.md)]显示和隐藏数据序列，如打开或关闭切换图例。
    
2. 鼠标指针悬停在图表中。 [!INCLUDE[name-sos](../includes/name-sos-short.md)]显示有关数据序列标签以及其值，如下面的屏幕截图中所示的详细信息。

   ![图表切换和图例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 快速开启使用内置的见解小组件示例见解小组件。
> * 查看表空间使用情况的详细信息。
> * 筛选数据，并在见解图表上查看标签的详细信息

若要了解如何构建自定义见解小组件，请完成下一教程：

> [!div class="nextstepaction"]
> [生成自定义见解小组件](tutorial-build-custom-insight-sql-server.md)。