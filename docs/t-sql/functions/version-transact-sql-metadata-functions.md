---
title: "版本 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ba4237f9a43a525571a2d25f95acb0a31d4a5cb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="version---transact-sql-metadata-functions"></a>版本-Transact SQL 元数据函数
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 返回的版本[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]在设备上运行。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 & #40;Transact SQL & #41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>参数  
  
## <a name="general-remarks"></a>一般备注  
必须在指定表名称[FROM](../../t-sql/queries/from-transact-sql.md)此函数可返回结果的子句。 将为中的查询; 的结果集的每一行返回的结果行使用[顶部 (Transact SQL)](../../t-sql/queries/top-transact-sql.md)来限制返回的行数。  
  
## <a name="examples"></a>示例  
下面的示例返回的版本号。  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>另请参阅 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
