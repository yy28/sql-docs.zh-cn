---
title: 从数据库 (OracleToSQL) 刷新 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: decc6e25cc8480dfaf041a79baa0972bdd78e569
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625857"
---
# <a name="refresh-from-database-oracletosql"></a>从数据库刷新 (OracleToSQL)
**从数据库刷新**对话框允许您选择要从 Oracle 数据库刷新的对象。 在对话框中的行进行了颜色编码基于元数据的状态：  
  
-   如果本地和 Oracle 数据库中已更改的对象元数据，该行是蓝色的。  
  
-   如果对象元数据已更改的 Oracle 数据库中但不是在 SSMA 中，该行是黄色。  
  
-   如果对象元数据已更改本地，但不是在 Oracle 数据库时，行是绿色。  
  
-   如果对象是 Oracle 数据库中的新增功能，该行是粉红色。  
  
可以指定默认值对象中的刷新设置**项目设置**对话框。 有关详细信息，请参阅[项目设置&#40;同步&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)。  
  
访问**从数据库刷新**对话框中，右键单击对象在 Oracle 元数据资源管理器中单击**从数据库刷新**。  
  
## <a name="options"></a>选项  
**折叠 （-）**  
折叠所有对象组，若要隐藏单独的对象。  
  
**展开 （+）**  
展开以显示单个对象的所有对象组。  
  
**隐藏/显示相同的对象**  
如果对象元数据相同的 Oracle 数据库中并在 SSMA 中将隐藏列表中的对象。  
  
**从数据库 （箭头按钮） 刷新**  
使用箭头按钮以指定应在 SSMA 中更新所选对象的元数据。  
  
**从数据库中执行不会刷新 (X 按钮）**  
使用 X 按钮以指定应在 SSMA 中更新所选对象的元数据。  
  
**图例**  
显示**图例**对话框。 图例包含行颜色和元数据状态之间的映射。  
  
若要保留**图例**对话框的顶部**从数据库刷新**对话框中，选择**在顶部显示**复选框。  
  
