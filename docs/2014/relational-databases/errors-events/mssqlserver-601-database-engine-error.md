---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0cb9c16487408f5be8598a7fee3c748efd8591e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127531"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|601|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|由于数据移动，无法继续以 NOLOCK 方式扫描。|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]无法继续执行查询，因为正在尝试读取由其他事务更新或删除的数据。 查询使用的是 NOLOCK 锁提示或 READ UNCOMMITTED 事务隔离级别。  
  
 通常，系统拒绝用户访问其他事务正在更改的数据，因为已锁定该数据。 但是，利用 NOLOCK 锁提示和 READ UNCOMMITTED 事务隔离级别，可以允许查询对其他事务锁定的数据进行读取。 这称为脏读，因为您可以读取尚未提交并且随时可能更改的值。  
  
## <a name="user-action"></a>用户操作  
 此错误取消了该查询。 重新提交该查询或删除 NOLOCK 锁提示。  
  
## <a name="see-also"></a>请参阅  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
