---
title: sp_syscollector_enable_collector （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_enable_collector
- sp_syscollector_enable_collector_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_enable_collector
- data collector [SQL Server], stored procedures
ms.assetid: 53ff2b0d-b7da-4e3d-8f3d-35e857bc3720
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 49ba4abf13978e16dc4a868843d23348dd38e64f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892896"
---
# <a name="sp_syscollector_enable_collector-transact-sql"></a>sp_syscollector_enable_collector (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  启用数据收集器。 由于每个服务器只有一个数据收集器，因此不需要任何参数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
dbo.sp_syscollector_enable_collector   
```  
  
## <a name="arguments"></a>参数  
 None  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 默认值为服务器上的数据收集器。  
  
## <a name="permissions"></a>权限  
 必须具有 **dc_admin** 或 **dc_operator** （拥有 EXECUTE 权限）固定数据库角色的成员身份才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例启用数据收集器。  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)  
  
  
