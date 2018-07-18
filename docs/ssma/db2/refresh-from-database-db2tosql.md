---
title: 刷新从数据库 (DB2ToSQL) |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f61bbf015c9c4a1dc0a650aa2299e763b00e7e62
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775323"
---
# <a name="refresh-from-database-db2tosql"></a>刷新从数据库 (DB2ToSQL)
**从数据库刷新**对话框中，可以选择要刷新从 DB2 数据库的对象。 在对话框中的行进行了颜色编码基于元数据的状态：  
  
-   如果在本地及 DB2 数据库中已更改的对象元数据，行显示为蓝色。  
  
-   如果在 DB2 数据库但不是在 SSMA，已更改的对象元数据，则行为黄色。  
  
-   如果对象元数据已更改本地，但不是在 DB2 数据库中，行为绿色。  
  
-   如果对象是 DB2 数据库中的新增功能，该行是粉红色。  
  
你可以指定中的默认对象刷新设置**项目设置**对话框。 有关详细信息，请参阅[项目设置&#40;同步&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
访问**从数据库刷新**对话框中，右键单击对象 DB2 元数据资源管理器中单击**从数据库刷新**。  
  
## <a name="options"></a>“常规”  
**折叠 （-）**  
折叠所有对象组，以隐藏的单个对象。  
  
**展开 （+）**  
展开要显示单个对象的所有对象组。  
  
**隐藏/显示相等的对象**  
隐藏对象从列表中的对象元数据是否相同和 SSMA DB2 数据库中。  
  
**刷新从数据库 （箭头按钮）**  
使用箭头按钮以指定应在 SSMA 更新所选对象的元数据。  
  
**从数据库中执行不刷新 (X 按钮）**  
X 按钮用于指定应在 SSMA 更新所选对象的元数据。  
  
**图例**  
显示**图例**对话框。 图例包含行颜色和元数据状态之间的映射。  
  
若要保留**图例**对话框的顶部**从数据库刷新**对话框中，选择**在顶部显示**复选框。  
  
