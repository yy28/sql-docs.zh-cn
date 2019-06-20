---
title: 扩展存储过程的执行特征 |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 93cb1b63e768623e39bcd5267c029a4ccb550c6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742413"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>扩展存储过程的执行特征
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 执行扩展存储过程具有以下特征：  
  
-   扩展存储的过程函数执行的安全上下文[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   扩展存储过程函数在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的进程空间中运行。  
  
-   与执行扩展存储过程关联的线程和用于客户端连接的线程相同。  
  
    > [!IMPORTANT]  
    >  在将扩展存储过程添加到服务器和授予其他用户执行权限之前，系统管理员应该彻底检查每个扩展存储过程以确保它不含有有害的或恶意的代码。  
  
-  
  
 扩展存储的过程加载 DLL 后，该 DLL 中保持加载状态之前的服务器的地址空间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已停止或管理员显式卸载该 DLL 使用 DBCC *DLL_name* （免费）。  
  
 使用 EXECUTE 语句，可以通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 将扩展存储过程作为存储过程来执行：  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parameters  
 \@ *retval*  
 是返回值。  
  
 \@ *param1*  
 输入参数。  
  
 \@ *param2*  
 输入/输出参数。  
  
> [!CAUTION]  
>  扩展存储过程提供性能增强功能，并扩展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 但是，由于扩展存储过程 DLL 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享相同的地址空间，发生问题的过程可能反过来影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行。 虽然扩展存储过程 DLL 引发的异常是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理的，但是仍可能损坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据区域。 作为一种安全预防措施，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员才能向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 添加扩展存储过程。 应彻底测试这些过程，然后才能进行安装。  
  
## <a name="see-also"></a>请参阅  
 [编写扩展存储的过程](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [查询 SQL Server 中安装的扩展存储过程](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
