---
title: "clr enabled 服务器配置选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "程序集 [CLR 集成], 验证是否可以运行"
  - "clr enabled 选项"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# clr enabled 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  可以使用 clr enabled 选项指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否可以运行用户程序集。 clr enabled 选项提供下列值： 
  
|值|说明|  
|-----------|-----------------|  
|0|不允许在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上执行程序集。|  
|1|允许在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上执行程序集。|  
  
仅 WOW64。 重启 WOW64 服务器使设置更改生效。 其他服务器类型不需要重启。  

运行 RECONFIGURE 时，clr enabled 选项的运行值将从 1 更改为 0，所有包含用户程序集的应用程序域将立即被卸载。  
  
>  **轻型池不支持执行公共语言运行时(CLR)**。禁用以下两个选项中的一个：“clr enabled”或“lightweight pooling”。 依赖于 CLR 并且在纤程模式下无法正常工作的功能包括：**hierarchy** 数据类型、复制和基于策略的管理。  
  
## 示例  
 下面的示例首先显示 clr enabled 选项的当前设置，然后通过将选项值设置为 1 启用该选项。 若要禁用该选项，请将此值设置为 0。  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## 另请参阅  
 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  