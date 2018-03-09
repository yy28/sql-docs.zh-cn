---
title: "使用见解小组件监视服务器和 SQL 操作 Studio （预览版） 中的数据库 |Microsoft 文档"
description: "了解 SQL 操作 Studio （预览版） 中的见解小组件。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d810e0b5ed89b93ac3d56a12758285fbd297092b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>管理服务器和数据库与见解中的小组件[!INCLUDE[name-sos](../includes/name-sos-short.md)]

见解小组件需要你使用来监视服务器和数据库的 TRANSACT-SQL (T-SQL) 查询并将它们转换成真知灼见可视化效果。 

Insights 是可自定义图表和图形添加到服务器和数据库监视仪表板。 查看在一眼即可见解的服务器和数据库，然后向下钻取更多详细信息，并且启动你定义的管理操作。 

你可以构建出色服务器和数据库管理仪表板类似于下面的示例：

![数据库仪表板](media/insight-widgets/database-dashboard.png)


若要在跳转，并开始创建不同类型的见解小组件，请查看以下教程：

- [生成自定义见解小组件](tutorial-build-custom-insight-sql-server.md)
- *启用内置见解小组件*
   - [启用性能监视见解](tutorial-qds-sql-server.md)
   - [启用表空间使用情况见解](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 查询 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]可以避免引入尚未其他语言或大量用户接口，所以它尝试使用最少的 JSON 配置使用 T-SQL 尽可能多地尝试。 使用 T-SQL 的配置见解小组件利用现有源的有用可以转换为真知灼见小组件的 T-SQL 查询的无数的数目。

见解小组件组成一个或两个 T-SQL 查询：
* *见解小组件查询*是必需的且在小组件中返回显示的数据的查询。
* *了解详细信息查询*是仅需要如果您创建的见解详细信息页。

见解小组件查询定义呈现计数、 图表或关系图的数据集。 了解详细信息查询用于列出相关见解中了解详细信息面板中的表格格式的详细信息。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]执行见解小组件查询，将查询结果集映射到图表的数据集，然后将其呈现。 当用户打开了某个见解的详细信息时，它将执行了解详细信息查询并输出在对话框内的网格视图中的结果。

基本理念都是一种方法中编写的 T-SQL 查询，以便它可作为数据集的计数、 图表和图形小组件。 

## <a name="summary"></a>“摘要”

T-SQL 查询，其结果集确定见解小组件行为。 为图表类型编写查询或将现有查询正确的图表类型映射是考虑的主要方面，若要生成有效的见解小组件。



## <a name="additional-resources"></a>其他资源
- [查询编辑器](tutorial-sql-editor.md)

