---
title: clr enabled 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45c72bc5b811fec8e5532d5d03d4552cc2e0d319
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786676"
---
# <a name="clr-enabled-server-configuration-option"></a>clr enabled 服务器配置选项
  可以使用 clr enabled 选项指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是否可以运行用户程序集。 clr enabled 选项提供下列值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|不允许在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上执行程序集。|  
|1|允许在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上执行程序集。|  
  
 在对此设置所做的更改生效前，必须重新启动 WOW64 服务器。 其他服务器类型不需要重新启动。  
  
> [!NOTE]  
>  运行 RECONFIGURE 时，clr enabled 选项的运行值将从 1 更改为 0，所有包含用户程序集的应用程序域将立即被卸载。  
  
> [!NOTE]  
>  轻型池不支持执行公共语言运行时 (CLR)。 禁用以下两个选项中的一个：“clr enabled”或“lightweight pooling”。 依赖于 CLR 并且在纤程模式下无法正常工作的功能包括：`hierarchy` 数据类型、复制和基于策略的管理。  
  
## <a name="example"></a>示例  
 下面的示例首先显示 clr enabled 选项的当前设置，然后通过将选项值设置为 1 启用该选项。 若要禁用该选项，请将此值设置为 0。  
  
```  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;  
  
```  
  
## <a name="see-also"></a>请参阅  
 [lightweight pooling 服务器配置选项](lightweight-pooling-server-configuration-option.md)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [lightweight pooling 服务器配置选项](lightweight-pooling-server-configuration-option.md)  
  
  
