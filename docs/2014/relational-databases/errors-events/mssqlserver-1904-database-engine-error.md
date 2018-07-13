---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbf9281bf87ed9b59c19fcc199e5bdc158857c17
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419526"
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1904|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|KEYCOUNT|  
|消息正文|表 '%.\*ls' 的 %S_MSG '%.*ls' 在 %S_MSG 键列表中具有 %d 个列名。 索引或统计信息键列列表的最大限制为 %d。|  
  
## <a name="explanation"></a>解释  
 指定索引或统计信息的键列列表超出了允许的最大列数。  
  
## <a name="user-action"></a>用户操作  
 修改键列的列表，使其中包含的列数小于指定的最大列数。  
  
 对于非聚集索引，请考虑使用 CREATE INDEX 语句中的 INCLUDE 子句，将列作为非键列添加到索引中。 使用此方法可避免超过当前的索引大小限值（即最多 16 个键列）。 有关详细信息，请参阅 [Create Indexes with Included Columns](../indexes/create-indexes-with-included-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)   
 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)  
  
  
