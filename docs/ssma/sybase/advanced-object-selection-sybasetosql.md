---
title: 高级对象选择 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d2baa90f-1b77-47ce-988d-1910c7c74103
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9735f73bf9afbab346c29d90cf5fc33fd06a48b2
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779173"
---
# <a name="advanced-object-selection-sybasetosql"></a>高级的对象选择 (SybaseToSQL)
**高级对象部分**对话框可以通过使用中的对象名称，字符串和子字符串筛选数据库对象，然后选择或取消选择这些对象。 SSMA 执行对所选对象的转换和迁移操作。  
  
若要访问此对话框中，在元数据资源管理器中，右键单击，然后选择**高级对象选择**。  
  
当你首次打开对话框中时，单击**显示子类别项**以显示包含元数据加载到项目中的所有对象。 然后，您可以输入字符串的项进行筛选。 例如，输入字符串"company"以显示包含该字符串名称的所有项。  
  
使用此对话框之前，你可能想要强制 SSMA 来加载所有元数据转换架构或保存该项目。  
  
## <a name="options"></a>“常规”  
**检查所有项**  
将添加所有项旁边的复选标记。 在元数据资源管理器中，将立即选择这些项。  
  
**取消选中所有项**  
中移除所有项旁边的复选标记。 将在元数据资源管理器立即清除这些项。  
  
**列表视图模式**  
显示筛选列表中的项。  
  
**表视图模式**  
显示筛选表中的项。  
  
**显示仅加载的项**  
切换类别或项的显示。 当选择此按钮时，SSMA 显示匹配的筛选器条件以及那些以前加载的所有项。 如果未选择此按钮，SSMA 显示类别文件夹。  
  
**Filter**  
输入你想要用于筛选项的字符串。 例如，若要查找包含字符串的所有可用项"ID"中的项名称，输入字符串"ID"中**筛选器**框。  
  
如果项匹配的筛选条件，则将显示的类别或项为 string 类型。 若要查看的匹配项，我们建议你单击**仅显示加载项**按钮。  
  
**清除筛选器**  
清除**筛选器**框。  
  
