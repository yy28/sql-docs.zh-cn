---
title: "SESSION_ID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2a0d500a-f6c8-490f-9abd-3ae824986404
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9089c21109d6eedb1cdae0082e1530e8d77d9dde
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回当前的 ID[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]会话。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>返回值  
 返回**nvarchar(32)**值。  
  
## <a name="general-remarks"></a>一般备注  
 建立连接时，将每个用户连接到分配的会话 ID。 它保存为连接的持续时间。 当连接结束时，被释放了会话 ID。  
  
 会话 ID 以字母字符 SID 开头。 这些都是区分大小写，当在中使用会话 ID 必须大写[!INCLUDE[DWsql](../../includes/dwsql-md.md)]命令。  
  
 你可以查询视图[sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/en-us/5b656c55-427f-4306-8bd9-9d7987c203d9)检索此函数与相同的信息。  
  
## <a name="examples"></a>示例  
 下面的示例返回当前会话 id。  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>另请参阅  
 [DB_NAME &#40;Transact SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [版本 &#40;SQL 数据仓库 &#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  

