---
title: 从数据库关系图中移除表 (Visual Database Tools) | Microsoft Docs
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
- deleting tables
- removing tables
- dropping tables
ms.assetid: 11afcfa1-816b-419c-9bc7-3abf366f4c3c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f7544d81e3503798203f702b4ff6a6ba88d6718
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="remove-tables-from-database-diagrams-visual-database-tools"></a>从数据库关系图中移除表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以从数据库关系图中移除表。 移除表不会更改数据库。 该表及其与其他表的关系将继续存在于数据库中。  
  
### <a name="to-remove-a-table-from-a-database-diagram"></a>从数据库关系图中移除表  
  
1.  在数据库关系图中，选择要移除的表。  
  
2.  右键单击该表，然后从快捷菜单中选择“从关系图中删除表”。  
  
    -或 -  
  
    按 Esc 键。  
  
    如果该表有未保存的更改（由于您在数据库关系图中编辑过它），则在移除该表之前，会显示一条消息，提示您保存该表。  
  
此时，已从关系图中移除了该表，但它会继续存在于数据库中。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[如何从数据库中删除表 (Visual Database Tools)](http://msdn.microsoft.com/en-us/ca6aa3e9-9885-44c3-bafc-aec441fd97ec)  
  
