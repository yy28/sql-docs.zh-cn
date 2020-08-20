---
description: 扩展存储过程的执行特征
title: 扩展存储过程的执行特征
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 23162895a2e2461fbd6f0f0abbe71341ce2fbf91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460855"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>扩展存储过程的执行特征
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 执行扩展存储过程具有以下特征：  
  
-   扩展存储过程函数在的安全上下文中执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   扩展存储过程函数在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的进程空间中运行。  
  
-   与执行扩展存储过程关联的线程和用于客户端连接的线程相同。  
  
    > [!IMPORTANT]  
    >  在将扩展存储过程添加到服务器和授予其他用户执行权限之前，系统管理员应该彻底检查每个扩展存储过程以确保它不含有有害的或恶意的代码。  
  
-  
  
 加载扩展存储过程 DLL 后，DLL 将在服务器的地址空间中保持加载状态，直到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止或管理员使用 DBCC *DLL_NAME* (免费) 显式卸载 DLL。  
  
 使用 EXECUTE 语句，可以通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 将扩展存储过程作为存储过程来执行：  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>参数  
 \@ *retval*  
 为返回值。  
  
 \@*param1*  
 输入参数。  
  
 \@*param2*  
 输入/输出参数。  
  
> [!CAUTION]  
>  扩展存储过程提供性能增强功能，并扩展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 但是，由于扩展存储过程 DLL 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享相同的地址空间，发生问题的过程可能反过来影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行。 虽然扩展存储过程 DLL 引发的异常是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理的，但是仍可能损坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据区域。 作为一种安全预防措施，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员才能向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 添加扩展存储过程。 应彻底测试这些过程，然后才能进行安装。  
  
## <a name="see-also"></a>另请参阅  
 [扩展存储过程编程](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [查询 SQL Server 中安装的扩展存储过程](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
