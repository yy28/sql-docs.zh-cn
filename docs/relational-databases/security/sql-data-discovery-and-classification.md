---
title: SQL 数据发现和分类 | Microsoft Docs
description: SQL 数据发现和分类
services: sql-server
documentationcenter: ''
author: giladm
manager: shaik
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-server
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 02/13/2018
ms.author: giladm
ms.openlocfilehash: eee9d5b920f422d000fa4e9cb8b78924cb55b466
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="sql-data-discovery-and-classification"></a>SQL 数据发现和分类
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

数据发现和分类引入了全新工具，并将其内置于 SQL Server Management Studio (SSMS)，以便发现数据库中的敏感数据并对其进行分类、标记和报告。
发现最敏感的数据（如商业、金融、医疗和 PII 等）并对其进行分类在组织的信息保护中可起到关键作用。 它可以充当基础结构，用于：
* 帮助满足数据隐私标准和监管符合性需求，如 GDPR。
* 控制对包含高度敏感数据的数据库/列的访问，并加强其安全性。


> [!NOTE]
> SQL Server 2008 及更高版本支持数据发现和分类。 有关 Azure SQL 数据库，请参阅 [Azure SQL 数据库数据发现和分类](https://go.microsoft.com/fwlink/?linkid=866265)。

## <a id="subheading-1"></a>概述
数据发现和分类引入了一套高级服务，形成了一种旨在保护各种数据（而不只是数据库）的全新 SQL 信息保护范例：
* 发现和建议 - 分类引擎扫描数据库，并标识包含潜在敏感数据的列。 利用它可以轻松查看和应用相应的分类建议，也可以手动对列进行分类。
* 标记 - 可以在列上永久地标记敏感度分类标签。
* 可见性 - 可以在详细报表中查看数据库分类状态，如在符合性和审核等事项中对其有需求，则可以直接打印/导出该报表。

## <a id="subheading-2"></a>发现、分类和标记敏感列
以下部分介绍如何在数据库中发现包含敏感数据的列并对其进行分类和标记、如何查看数据库的当前分类状态，以及如何导出报表。

分类包含两种元数据属性：
* 标签 - 这是主要的分类属性，用于定义存储在列中的数据的敏感度级别。  
* 信息类型 - 为列中存储的数据类型提供额外的粒度。

<br>
**对 SQL Server 数据库进行分类：**

1. 在 SQL Server Management Studio (SSMS) 中连接到 SQL Server。

2. 在 SSMS 对象资源管理器中，右键单击要分类的数据库，并选择“任务” > “对数据进行分类...”。

    ![“导航”窗格][1]

3. 分类引擎扫描数据库，寻找包含潜在敏感数据的列，并提供“建议的列分类”列表：

    * 要查看建议的列分类列表，请单击窗口顶部的建议通知框，或底部的建议面板：

        ![“导航”窗格][2]

        ![“导航”窗格][3]

    * 查看建议列表：
        * 要接受针对某特定列的建议，请选中相关行左侧列中的复选框。 还可以选中建议表标头中的复选框，将所有建议标记为“接受”。

        * 也可以使用下拉框更改建议的信息类型和敏感度标签。        

        ![“导航”窗格][4]

    * 要应用所选建议，请单击蓝色的“接受所选建议”按钮。

        ![“导航”窗格][5]

4. 此外，还可以手动对列进行分类，或基于建议分类：

    * 单击窗口顶部菜单中的“添加分类”。

        ![“导航”窗格][6]

    * 在打开的上下文窗口中，选择要分类的“架构”>“表”>“列”，并选择信息类型和敏感度标签。 然后单击上下文窗口底部的蓝色“添加分类”按钮。

        ![“导航”窗格][7]

5. 要完成分类，并永久地使用新分类元数据标记数据库列，请在窗口顶部菜单中单击“保存”。

    ![“导航”窗格][8]


6. 要生成数据库分类状态的完整摘要报表，请在窗口顶部菜单中单击“查看报表”。

    ![“导航”窗格][9]

    ![“导航”窗格][10]


## <a id="subheading-3"></a>后续步骤

有关 Azure SQL 数据库，请参阅 [Azure SQL 数据库数据发现和分类](https://go.microsoft.com/fwlink/?linkid=866265)。

请考虑通过应用列级别安全性机制来保护敏感列：

* 用于模糊化使用中的敏感列的[动态数据掩码](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking)。
* 用于静态加密敏感列的 [Always Encrypted](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine)。

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Next Steps]: #subheading-3

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
