---
title: 从数据库 (DB2ToSQL) 刷新 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ef7778854248f194c01254b9cd6f833f67e9cefc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685115"
---
# <a name="refresh-from-database-db2tosql"></a>从数据库 (DB2ToSQL) 刷新
**从数据库刷新**对话框允许您选择要从 DB2 数据库刷新的对象。 在对话框中的行进行了颜色编码基于元数据的状态：  
  
-   如果本地和 DB2 数据库中已更改的对象元数据，该行是蓝色的。  
  
-   如果对象元数据已更改 DB2 数据库中但不是在 SSMA 中，该行是黄色。  
  
-   如果对象元数据已更改本地，但不是在 DB2 数据库中，行是绿色。  
  
-   如果对象是 DB2 数据库中的新增功能，该行是粉红色。  
  
可以指定默认值对象中的刷新设置**项目设置**对话框。 有关详细信息，请参阅[项目设置&#40;同步&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
访问**从数据库刷新**对话框中，右键单击对象在 DB2 元数据资源管理器中单击**从数据库刷新**。  
  
## <a name="options"></a>选项  
**折叠 （-）**  
折叠所有对象组，若要隐藏单独的对象。  
  
**展开 （+）**  
展开以显示单个对象的所有对象组。  
  
**隐藏/显示相同的对象**  
如果对象元数据是相同的 DB2 数据库中和在 SSMA 中将隐藏列表中的对象。  
  
**从数据库 （箭头按钮） 刷新**  
使用箭头按钮以指定应在 SSMA 中更新所选对象的元数据。  
  
**从数据库中执行不会刷新 (X 按钮）**  
使用 X 按钮以指定应在 SSMA 中更新所选对象的元数据。  
  
**图例**  
显示**图例**对话框。 图例包含行颜色和元数据状态之间的映射。  
  
若要保留**图例**对话框的顶部**从数据库刷新**对话框中，选择**在顶部显示**复选框。  
  
