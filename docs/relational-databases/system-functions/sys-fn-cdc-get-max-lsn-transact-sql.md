---
title: sys.fn_cdc_get_max_lsn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn_TSQL
- sys.fn_cdc_get_max_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_max_lsn
- sys.fn_cdc_get_max_lsn
ms.assetid: 93f3a4c8-b91f-4ebb-8e96-9397bb3a1c43
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fae4f476005cb227b198b193712e4a564a1418fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789955"
---
# <a name="sysfncdcgetmaxlsn-transact-sql"></a>sys.fn_cdc_get_max_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从的 start_lsn 列中返回的最大日志序列号 (LSN) [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)系统表。 您可以使用此函数为任何捕获实例返回变更数据捕获时间线的高端点。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## <a name="return-types"></a>返回类型  
 **binary(10)**  
  
## <a name="remarks"></a>备注  
 此函数的 start_lsn 列中返回的最大 LSN [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)表。 同样，它也是将更改传播到数据库更改表时捕获进程最后处理的 LSN。 它用作与为数据库定义的捕获实例相关联的所有时间线的高端点。  
  
 该函数通常用于获取查询间隔内的相应高端点。  
  
## <a name="permissions"></a>Permissions  
 要求具有公用数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-maximum-lsn-value"></a>A. 返回最大的 LSN 值  
 下例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中所有捕获示例的最大 LSN。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### <a name="b-setting-the-high-endpoint-of-a-query-range"></a>B. 设置查询范围的高端点  
 下面的示例使用 `sys.fn_cdc_get_max_lsn` 返回的最大 LSN 为捕获示例 `HumanResources_Employee` 设置查询范围的高端点。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
