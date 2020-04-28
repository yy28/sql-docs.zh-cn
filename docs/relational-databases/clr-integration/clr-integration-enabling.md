---
title: 启用 CLR 集成 |Microsoft Docs
description: 托管 CLR Microsoft SQL Server 称为 CLR 集成，默认情况下已禁用。 使用 sp_configure 存储过程来启用 CLR 集成。
ms.custom: ''
ms.date: 09/17/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d161135c8c8b0c7d7932eb08aa98509efc4bc45
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488098"
---
# <a name="clr-integration---enabling"></a>CLR 集成 - 启用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  默认情况下关闭公共语言运行时 (CLR) 集成功能，必须启用该功能才能使用借助 CLR 集成实现的对象。 若要启用 CLR 集成，请使用中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的**sp_configure**存储过程的**CLR enabled**选项：  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 可以通过将 " **clr 已启用**" 选项设置为0来禁用 clr 集成。 禁用 CLR 集成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]停止执行所有用户定义的 CLR 例程并卸载所有应用程序域。 依赖于 CLR 的功能（如**hierarchyid**数据类型、 `FORMAT`函数、复制和基于策略的管理）不受此设置的影响，并且将继续工作。
  
> [!NOTE]  
>  若要启用 CLR 集成，必须具有 ALTER SETTINGS 服务器级别权限，该权限由**sysadmin**和**serveradmin**固定服务器角色的成员隐式持有。  
  
> [!NOTE]  
>  配置使用大量内存空间和大量处理器的计算机可能在启动 SQL Server 时无法加载其中的 CLR 集成功能。 若要解决此问题，请使用 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务启动选项启动服务器，并指定足够大的内存值。 有关详细信息，请参阅 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  轻型池不支持执行公共语言运行时 (CLR)。 启用 CLR 集成之前，必须禁用轻型池。 有关详细信息，请参阅 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled 服务器配置选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-sql&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [服务器级角色](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
