---
title: 启用 CLR 集成 |微软文档
description: 托管 CLR 的 Microsoft SQL 服务器称为 CLR 集成，默认情况下禁用该集成。 使用sp_configure存储过程启用 CLR 集成。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488098"
---
# <a name="clr-integration---enabling"></a>CLR 集成 - 启用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  默认情况下关闭公共语言运行时 (CLR) 集成功能，必须启用该功能才能使用借助 CLR 集成实现的对象。 要启用 CLR 集成，请使用 sp_configure**存储过程**的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**clr 启用**选项，  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 通过将**启用 clr**的选项设置为 0，可以禁用 CLR 集成。 禁用 CLR 集成时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请停止执行所有用户定义的 CLR 例程并卸载所有应用程序域。 依赖于 CLR 的功能（如**层次结构数据类型**、`FORMAT`功能、复制和基于策略的管理）不受此设置的影响，并将继续运行。
  
> [!NOTE]  
>  要启用 CLR 集成，您必须具有 ALTER SETTINGS 服务器级别权限，该权限由**系统管理员**和**服务器管理员**固定服务器角色的成员隐式持有。  
  
> [!NOTE]  
>  配置使用大量内存空间和大量处理器的计算机可能在启动 SQL Server 时无法加载其中的 CLR 集成功能。 要解决此问题，请使用 **-gmemory_to_reserve**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务启动选项启动服务器，并指定足够大的内存值。 有关详细信息，请参阅 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  轻型池不支持执行公共语言运行时 (CLR)。 启用 CLR 集成之前，必须禁用轻型池。 有关详细信息，请参阅 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [启用 clr 服务器配置选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [重新配置&#40;转瞬端-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [&#40;转算-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [服务器级角色](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
