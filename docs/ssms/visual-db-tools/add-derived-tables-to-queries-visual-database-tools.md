---
title: 向查询中添加派生表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [Visual Database Tools]
- joins [SQL Server], derived tables
- table joins [SQL Server]
- derived tables
ms.assetid: 05f1ba1d-465f-4e36-84bb-21b963c9b8f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e21d05f42eaf41d932c82c7f24f63df9d42c8a9e
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699485"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>向查询中添加派生表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
派生表是结果集，在查询中用作表源。 可以在“关系图”窗格中将派生表添加到查询。  
  
### <a name="to-add-a-derived-table-to-a-query"></a>将派生表添加到查询  
  
1.  打开现有查询或创建新查询。  
  
2.  右键单击“关系图”窗格并选择“添加新派生表”。  
  
    将添加一个名为 derivedtbl_N 的新表，派生表的 SELECT 语句会添加到查询的 FROM 子句。  
  
## <a name="see-also"></a>另请参阅  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[创建查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[打开查询 (Visual Database Tools)](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)  
[SELECT (Transact-SQL)](https://msdn.microsoft.com/dc85caea-54d1-49af-b166-f3aa2f3a93d0)  
  
