---
title: DROP SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cdfe95b14e8005cb4086b909aea6a5cfb0bbd0cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从指定架构中删除一个同义词。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>参数  
 IF EXISTS  
适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）
  
 只有在同义词已存在时才对其进行有条件地删除。  
  
 *schema*  
 指定同义词所在的架构。 如果未指定架构，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将使用当前用户的默认架构。  
  
 *synonym_name*  
 要删除的同义词的名称。  
  
## <a name="remarks"></a>Remarks  
 对同义词的引用不受架构限制；因此，可随时删除同义词。 只有在运行时才能发现对已删除的同义词的引用。  
  
 在动态 SQL 中可以创建、删除和引用同义词。  
  
## <a name="permissions"></a>权限  
 若要删除同义词，用户必须至少满足以下条件之一。 用户必须是：  
  
-   同义词的当前拥有者。  
  
-   同义词的 CONTROL 权限拥有者。  
  
-   包含架构的 ALTER SCHEMA 权限的拥有者。  
  
## <a name="examples"></a>示例  
 以下示例将先创建一个同义词 `MyProduct`，然后再删除该同义词。  
  
```  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SYNONYM (Transact-SQL)](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
