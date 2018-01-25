---
title: "筛选设置（对象资源管理器和实用工具资源管理器）| Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-objects
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 049d826cfe7170462ed3942202f208a621362613
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>筛选设置（对象资源管理器和实用工具资源管理器）
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用此对话框可以指定筛选器。 使用筛选器，可以将对象资源管理器和实用工具资源管理器配置为仅显示符合特定条件的项。 例如，可以使用筛选器仅显示名称中包含词语“维护”的作业。 “筛选设置”对话框的标题包含服务器的名称，还可能包含数据库的名称。  
  
## <a name="uielement-list"></a>UIElement 列表  
**属性**  
显示要筛选的属性。  
  
**“运算符”**  
选择筛选器将值应用于属性的方式。 下面是可用的选项：  
  
-   **等于**  
  
    筛选器将显示属性和值都精确匹配的项。  
  
-   **包含**  
  
    筛选器将显示属性包含指定值的项。 属性可能会包含其他文本。  
  
-   **不包含**  
  
    筛选器将显示属性不包含指定值的项。  
  
-   **小于**  
  
    此筛选器适用于日期，将显示日期早于指定值的项。  
  
-   **小于或等于**  
  
    此筛选器适用于日期，将显示日期早于或等于指定值的项。  
  
-   **大于**  
  
    此筛选器适用于日期，将显示日期晚于指定值的项。  
  
-   **大于或等于**  
  
    此筛选器适用于日期，将显示日期晚于或等于指定值的项。  
  
-   **Between**  
  
    此筛选器适用于日期，将显示日期介于指定的两个日期之间的项。 选择“介于”并按 Tab 即可添加另一行，用于指定第二个日期。  
  
-   **不介于**  
  
    此筛选器适用于日期，将显示日期不介于指定的两个日期之间的项。 选择“不介于”并按 Tab 移出“运算符”列，即可添加另一行，用于指定第二个日期。  
  
**ReplTest1**  
键入要与属性进行比较的值。 对于日期，请单击下箭头显示日历，以选择日期。  
  
**清除筛选器**  
删除所有当前筛选设置。  
  
## <a name="see-also"></a>另请参阅  
[使用 SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[SQL Server 实用工具概述](http://msdn.microsoft.com/en-us/6e6cbd25-6b1c-4e21-9ade-4584e243fd8f)  
  
