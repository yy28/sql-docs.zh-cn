---
title: 高级对象选择 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ca098c15-c343-4d7d-a284-c2fc405eb991
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 46e1bdc5b9fdfbbe9c804b4bf2214b9c04b6cdac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453495"
---
# <a name="advanced-object-selection-db2tosql"></a>高级的对象选择 (DB2ToSQL)
**高级对象部分**对话框可以通过使用字符串和子字符串中的对象名称，来筛选数据库对象，然后选择或取消选择这些对象。 SSMA 执行对所选对象的转换和迁移操作。  
  
要访问此对话框中，在元数据资源管理器中，右键单击，然后选择**高级对象选择**。  
  
当你首次打开对话框中时，单击**显示子类别项**显示具有元数据加载到项目中的所有对象。 然后，可以输入字符串的项进行筛选。 例如，输入"公司"以显示包含该字符串的名称的所有项的字符串。  
  
使用此对话框之前，你可能想要强制 SSMA 来加载转换架构或保存项目的所有元数据。  
  
## <a name="options"></a>选项  
**选中所有项**  
添加所有项旁边的复选标记。 将元数据资源管理器中立即选择这些项。  
  
**取消选中所有项**  
移除所有项旁边的复选标记。 这些项将被立即清除元数据资源管理器中。  
  
**列表视图模式**  
显示筛选列表中的项。  
  
**表视图模式**  
显示筛选的表中的项。  
  
**显示仅加载的项**  
切换类别或项的显示。 选中此按钮后，SSMA 显示匹配的筛选器条件和先前加载的所有项。 如果未选择此按钮，SSMA 显示类别文件夹。  
  
**Filter**  
输入想要用于筛选项的字符串。 例如，若要查找所有可用的项包含字符串"ID"项名称中，输入字符串"ID"中**筛选器**框。  
  
如果项匹配的筛选条件，则将显示的类别或项为键入的字符串。 若要查看匹配项，我们建议您单击**仅显示加载项**按钮。  
  
**清除筛选器**  
清除**筛选器**框。  
  
