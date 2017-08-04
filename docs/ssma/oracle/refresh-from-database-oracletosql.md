---
title: "刷新从数据库 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 536fa920910c56698be8b161f59294f555747917
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="refresh-from-database-oracletosql"></a>刷新从数据库 (OracleToSQL)
**从数据库刷新**对话框中，可以选择要从 Oracle 数据库刷新的对象。 在对话框中的行进行了颜色编码基于元数据的状态：  
  
-   如果本地和 Oracle 数据库中已更改的对象元数据，行显示为蓝色。  
  
-   如果对象元数据已更改的 Oracle 数据库中但不是在 SSMA，该行是黄色。  
  
-   如果对象元数据已更改本地，但不是在 Oracle 数据库中，行为绿色。  
  
-   如果对象是新的 Oracle 数据库中，行是粉红色。  
  
你可以指定中的默认对象刷新设置**项目设置**对话框。 有关详细信息，请参阅[项目设置 &#40;同步 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
访问**从数据库刷新**对话框中，右键单击对象 Oracle 元数据资源管理器中单击**从数据库刷新**。  
  
## <a name="options"></a>选项  
**折叠 （-）**  
折叠所有对象组，以隐藏的单个对象。  
  
**展开 （+）**  
展开要显示单个对象的所有对象组。  
  
**隐藏/显示相等的对象**  
如果对象元数据相同的 Oracle 数据库中和在 SSMA 将隐藏从列表中的对象。  
  
**刷新从数据库 （箭头按钮）**  
使用箭头按钮以指定应在 SSMA 更新所选对象的元数据。  
  
**从数据库中执行不刷新 (X 按钮）**  
X 按钮用于指定应在 SSMA 更新所选对象的元数据。  
  
**图例**  
显示**图例**对话框。 图例包含行颜色和元数据状态之间的映射。  
  
若要保留**图例**对话框的顶部**从数据库刷新**对话框中，选择**在顶部显示**复选框。  
  

