---
title: "对象层次结构语法 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 23464c196392c8be8eee21ca37e6ee1adb1d2ebb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="object-hierarchy-syntax-transact-sql"></a>对象层次结构语法 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *Propertyname* sp_OASetProperty sp_OAGetProperty 以及参数和*methodname* sp_OAMethod 参数支持类似于的对象层次结构语法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. 当使用该特殊语法时，这些参数具有以下通用格式。  
  
## <a name="syntax"></a>语法  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>参数  
 *TraversedObject*  
 是下的层次结构中的 OLE 对象*objecttoken*在存储过程中指定。 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 语法指定一系列集合、对象属性和返回对象的方法。 该系列中的每个对象说明符必须用句号 (.) 分隔。  
  
 系列中的项可以是集合名。 使用下面的语法指定集合：  
  
 集合 ("*项*")  
  
 要求使用双引号 (")。 不支持用于集合的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 惊叹号 (!) 语法。  
  
 *PropertyOrMethod*  
 属性的名称或方法的*TraversedObject*。  
  
 若要通过使用 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 参数（包括对 sp_OAMethod 输出参数的支持）指定所有索引或方法参数，请使用下面的语法：  
  
 *PropertyOrMethod*  
  
 若要在圆括号内指定所有索引或方法参数（将导致忽略 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 的所有索引或方法参数），请使用下面的语法：  
  
 *PropertyOrMethod*([ *ParameterName*: =]"*参数*"[，...])  
  
 要求使用双引号 (")。 指定了所有位置参数后，才能指定命名参数。  
  
## <a name="remarks"></a>注释  
 如果*TraversedObject*未指定， *PropertyOrMethod*是必需的。  
  
 如果*PropertyOrMethod*未指定， *TraversedObject*从 OLE 自动化存储过程返回作为对象令牌输出参数。 如果*PropertyOrMethod*指定的属性或方法的*TraversedObject*调用时，和属性值或方法返回值作为输出参数返回从 OLE 自动化存储的过程。  
  
 如果任一项中*TraversedObject*列表不会返回 OLE 对象，将引发错误。  
  
 有关 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE 对象语法的详细信息，请参阅 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 文档。  
  
 有关 HRESULT 返回代码的详细信息，请参阅[sp_OACreate &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md).  
  
## <a name="examples"></a>示例  
 以下是使用 SQL-DMO SQLServer 对象的对象层次结构语法的示例。  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>另请参阅  
 [OLE 自动化脚本示例](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE 自动存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
