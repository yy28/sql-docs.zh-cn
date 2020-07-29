---
title: 从数据库关系图中移除表
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
ms.assetid: 11afcfa1-816b-419c-9bc7-3abf366f4c3c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 40d205f0f1f638814b8b2c91efaf18c26473eda8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999452"
---
# <a name="remove-tables-from-database-diagrams-visual-database-tools"></a>从数据库关系图中移除表 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以从数据库关系图中移除表。 移除表不会更改数据库。 该表及其与其他表的关系将继续存在于数据库中。  
  
### <a name="to-remove-a-table-from-a-database-diagram"></a>从数据库关系图中移除表  
  
1.  在数据库关系图中，选择要移除的表。  
  
2.  右键单击该表，然后从快捷菜单中选择“从关系图中删除表”  。  
  
    -或-  
  
    按 Esc 键。  
  
    如果该表有未保存的更改（由于您在数据库关系图中编辑过它），则在移除该表之前，会显示一条消息，提示您保存该表。  
  
此时，已从关系图中移除了该表，但它会继续存在于数据库中。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[如何：从数据库中删除表 (https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec)  
  
