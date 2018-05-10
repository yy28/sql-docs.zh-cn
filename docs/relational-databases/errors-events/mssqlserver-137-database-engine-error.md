---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d581cb6eeeb0965143b4830f90c0c537d4db7db
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|137|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|P_SCALAR_VAR_NOTFOUND|  
|消息正文|必须声明标量变量 "%.*ls"。|  
  
## <a name="explanation"></a>解释  
如果未首先声明某个变量就在 SQL 脚本中使用它，则会出现此错误。 在下面的示例中，由于未声明 **@mycol**，因此针对 SET 和 SELECT 语句都将返回 137 错误。  
  
SET @mycol = 'ContactName';  
  
SELECT @mycol;  
  
之所以发生此错误，一个更为复杂的原因就是使用在 EXECUTE 语句外部声明的变量。 例如，在 SELECT 语句中指定的变量 **@mycol** 是 SELECT 语句的局部变量，因此它位于 EXECUTE 语句外部。  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>用户操作  
确认先声明 SQL 脚本中所使用的任何变量，然后再将其用在脚本中的其他位置。  
  
重新编写该脚本，以便不在 EXECUTE 语句中引用在其外部声明的变量。 例如：  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>另请参阅  
[EXECUTE (Transact-SQL)](~/t-sql/language-elements/execute-transact-sql.md)  
[SET 语句 (Transact-SQL)](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
