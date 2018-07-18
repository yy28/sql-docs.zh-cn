---
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a71eaec07e5516c0e8e9d33b9f026cc078d88e7d
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37792058"
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact SQL 元数据函数
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 返回在设备上运行的 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 的版本。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>参数  
  
## <a name="general-remarks"></a>一般备注  
必须在 [FROM](../../t-sql/queries/from-transact-sql.md) 子句中指定表名称，此函数才会返回结果。 对于该查询的结果集中的每一行，都会返回结果行，使用 [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) 可限制返回的行数。  
  
## <a name="examples"></a>示例  
下面的示例返回版本号。  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>另请参阅 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME (Transact-SQL)](../../t-sql/functions/db-name-transact-sql.md)  
  
  
