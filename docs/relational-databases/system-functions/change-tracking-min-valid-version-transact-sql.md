---
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0a37a969a2a5e0f7cfb6586549e78eb8b36c4fa0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062969"
---
# <a name="changetrackingminvalidversion-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在使用中时获取更改跟踪信息从指定的表中，使用时有效的客户端上返回的最低版本[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)函数。  
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>参数  
 *table_object_id*  
 是表的对象 ID。 *table_object_id*是**int**。  
  
## <a name="return-type"></a>返回类型  
 **bigint**  
  
## <a name="remarks"></a>Remarks  
 使用此函数可验证的值*last_sync_version* CHANGETABLE 的参数。 如果*last_sync_version*小于报告的此函数中，从稍后调用 CHANGETABLE 返回的结果可能不是有效的值。  
  
 CHANGE_TRACKING_MIN_VALID_VERSION 使用以下信息来确定返回值：  
  
-   为此表启用更改跟踪的时间。  
  
-   何时运行后台清除任务来删除超过了数据库的指定保持期的更改跟踪信息。  
  
-   此表是否已被截断。 这会删除与此表关联的所有更改跟踪信息。  
  
 如果符合下列任一条件，该函数将返回 NULL：  
  
-   没有为数据库启用更改跟踪。  
  
-   指定表的对象 ID 对当前数据库无效。  
  
-   对由此对象 ID 指定的表拥有的权限不足。  
  
## <a name="examples"></a>示例  
 下面的示例确定指定的版本是否为有效版本。 此示例获取 `dbo.Employees` 表的最低有效版本，然后将其与 `@last_sync_version` 变量的值进行比较。 如果 `@last_sync_version` 的值低于 `@min_valid_version` 的值，则已更改行的列表将无效。  
  
> [!NOTE]  
>  通常，您可以从存储用来同步数据的上一个版本号的表或其他位置获取此值。  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>请参阅  
 [变更跟踪函数 (Transact-SQL)](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables (Transact-SQL)](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
