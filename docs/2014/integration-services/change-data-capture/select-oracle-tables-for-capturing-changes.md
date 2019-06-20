---
title: 为捕获更改选择 Oracle 表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0b962db5e005837a2e9d3fe68564fceb5bfc253
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835262"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>为捕获更改选择 Oracle 表
  使用此对话框可选择在 CDC 实例中包含的表。 所选表将添加到新建实例向导的 **“选择表和列”** 页的列表中。 可以在此对话框中执行以下操作。  
  
 默认情况下，此对话框的表的列表中不包含任何表。 您可以选中复选框列顶部的复选框，以便选择所有表或搜索特定表。  
  
 **搜索特定表**  
 按如下所示输入搜索条件，然后单击“搜索”  ：  
  
-   **架构**：从列表中选择数据库架构。 只有具有该架构的表才会出现在列表中。  
  
-   **表名称模式**：输入任意字符的字符串。 将仅显示包含输入的字符串的表。  
  
> [!NOTE]  
>  您可以在其中一个或全部两个字段中输入条件。  
  
-   **显示前 1000 个匹配表**：默认情况下，此复选框处于选中状态。 它将显示限制为前 1000 个匹配表。 如果取消选中该复选框，将显示条件相匹配的所有表。 如果有大量的表，则此方法可能需要较长的时间来显示列表。  
  
 **选择要包括在 CDC 实例中的表**  
 单击要包含的任何表旁边的复选框，然后单击“添加”  。 相应的表将添加到新建实例向导的 **“选择表和列”** 页的列表中。  
  
 单击 **“关闭”** 将关闭该对话框并且不再添加任何表。  
  
> [!NOTE]  
>  如果您选择包含不支持的数据类型的表，将会看到一条错误消息，并且将不会包含该表。  
  
## <a name="see-also"></a>请参阅  
 [如何创建 SQL Server 更改数据库实例](how-to-create-the-sql-server-change-database-instance.md)   
 [选择 Oracle 表和列](select-oracle-tables-and-columns.md)  
  
  
