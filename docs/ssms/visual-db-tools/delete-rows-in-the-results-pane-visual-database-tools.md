---
title: 在“结果”窗格中删除行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: faa65ae62d27c5015301303a947996323a4fb785
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33050534"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>在“结果”窗格中删除行 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果希望删除数据库中的记录，请在“结果”窗格中删除相应的行。 如果希望删除所有行，则可以使用“删除”查询。 有关详细信息，请参阅 [创建“删除”查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)。 如果只希望将行从“结果”窗格中移除，请更改查询的条件。 有关详细信息，请参阅 [指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
### <a name="to-delete-a-row-or-rows"></a>删除一行或多行  
  
1.  在“结果”窗格中选中要删除的行左侧的框。  
  
2.  按 Delete。  
  
3.  在要求确认的消息框中单击“是”。  
  
> [!CAUTION]  
> 以这种方式删除的行将从数据库中永久移除并且不能恢复。  
  
> [!NOTE]  
> 如果所选行中有任意行无法从数据库中删除，则这些行都不会删除，并且系统将显示消息，指示无法删除哪些行。  
  
## <a name="see-also"></a>另请参阅  
[创建“删除”查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
