---
title: 使用见解小组件来监视服务器和 Azure Data Studio 中的数据库 |Microsoft Docs
description: 了解如何在 Azure Data Studio 见解小组件。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d669b72aadb9fe1ea2ec61c2059a1d932ee52d4d
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356328"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>管理服务器和见解小组件中使用的数据库 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

见解小组件需要使用来监视服务器和数据库的 TRANSACT-SQL (T-SQL) 查询并将其转换为见解深刻的可视化效果。 

Insights 是可自定义图表和图形添加到服务器和数据库监视仪表板。 查看一眼见解的服务器和数据库，然后深入了解更多详细信息，并启动的已定义的管理操作。 

您可以构建令人惊叹服务器和数据库管理仪表板类似于下面的示例：

![数据库仪表板](media/insight-widgets/database-dashboard.png)


若要在跳转，并开始创建不同类型的见解小组件，请查看以下教程：

- [生成自定义见解小组件](tutorial-build-custom-insight-sql-server.md)
- *启用内置见解小组件*
   - [启用性能监视见解](tutorial-qds-sql-server.md)
   - [启用表空间使用情况见解](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 查询 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 尝试避免引入但另一个语言或大量用户界面以便尝试使用 T-SQL 尽可能多地使用最小 JSON 配置。 使用 T-SQL 配置见解小组件利用无数的现有源的查询可以转换为见解深刻的小组件的非常有用的 T-SQL 查询数。

见解小组件组成一个或两个 T-SQL 查询：
* *见解小组件查询*是必需的并且是在小组件中返回显示的数据的查询。
* *了解详细信息查询*是仅在需要创建一个了解详细信息页。

见解小组件查询定义呈现计数、 图表或图形的数据集。 了解详细信息查询用于列出相关的见解以了解详细信息面板中的表格格式的详细信息。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 执行见解小组件查询并将查询结果集映射到图表的数据集，然后将其呈现。 当用户打开了某个见解的详细信息时，它执行了解详细信息查询，并打印出在对话框中的网格视图中的结果。

基本理念是一种方法中编写 T-SQL 查询，以便它可以用作数据集的计数、 图表和图形小组件。 

## <a name="summary"></a>“摘要”

T-SQL 查询，其结果集确定见解小组件行为。 编写查询的图表类型或映射正确的图表类型的现有查询是关键的考虑因素，以生成有效的见解小组件。



## <a name="additional-resources"></a>其他资源
- [查询编辑器](tutorial-sql-editor.md)

