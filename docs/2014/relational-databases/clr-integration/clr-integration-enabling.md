---
title: 启用 CLR 集成 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15ad6087fc711de1ab818b10d591cd48512bb9a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124349"
---
# <a name="enabling-clr-integration"></a>启用 CLR 集成
  默认情况下关闭公共语言运行时 (CLR) 集成功能，必须启用该功能才能使用借助 CLR 集成实现的对象。 若要启用 CLR 集成，请使用**启用 clr**选项**sp_configure**存储过程：  
  
```  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 你可以通过设置来禁用 CLR 集成**启用 clr**为 0 的选项。 禁用 CLR 集成后，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 停止执行所有 CLR 例程并卸载所有应用程序域。  
  
> [!NOTE]  
>  若要启用 CLR 集成，你必须具有 ALTER SETTINGS 服务器级别权限，该权限的成员隐式具有**sysadmin**和**serveradmin**固定服务器角色的成员。  
  
> [!NOTE]  
>  配置使用大量内存空间和大量处理器的计算机可能在启动 SQL Server 时无法加载其中的 CLR 集成功能。 若要解决此问题，启动服务器，通过使用 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务启动选项，并指定一个足够大的内存值。 有关详细信息，请参阅 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  轻型池不支持执行公共语言运行时 (CLR)。 启用 CLR 集成之前，必须禁用轻型池。 有关详细信息，请参阅 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>请参阅  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [clr enabled 服务器配置选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)   
 [服务器级角色](../security/authentication-access/server-level-roles.md)  
  
  
