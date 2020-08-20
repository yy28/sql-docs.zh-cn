---
description: sp_syscollector_disable_collector (Transact-SQL)
title: sp_syscollector_disable_collector (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_disable_collector_TSQL
- sp_syscollector_disable_collector
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_disable_collector
ms.assetid: 9ef4c85d-cca6-452d-94be-2be6f616c3d8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e8f3e60112ed2f7e96d95652d370dac5fca44b80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463979"
---
# <a name="sp_syscollector_disable_collector-transact-sql"></a>sp_syscollector_disable_collector (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  禁用数据收集器。 由于每个服务器只有一个数据收集器，因此不需要任何参数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
dbo.sp_syscollector_disable_collector   
```  
  
## <a name="arguments"></a>参数  
 无  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 默认值为服务器上的数据收集器。  
  
## <a name="permissions"></a>权限  
 必须具有 **dc_admin** 或 **dc_operator** （拥有 EXECUTE 权限）固定数据库角色的成员身份才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例禁用数据收集器。  
  
```  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
