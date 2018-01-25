---
title: "删除外部数据源 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: "14"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b479c5fd28b97eb6fae75d9490a52c9e56c3fa7f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-data-source-transact-sql"></a>DROP EXTERNAL DATA SOURCE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  删除 PolyBase 外部数据源。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *external_data_source_name*  
 要删除的外部数据源的名称。  
  
## <a name="metadata"></a>元数据  
 若要查看列表的外部数据源，请使用 sys.external_data_sources 系统视图。  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>权限  
 需要更改任何外部数据源。  
  
## <a name="locking"></a>锁定  
 外部数据源对象上采用共享的锁。  
  
## <a name="general-remarks"></a>一般备注  
 删除外部数据源不会删除外部数据。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-basic-syntax"></a>A. 使用基本语法  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

