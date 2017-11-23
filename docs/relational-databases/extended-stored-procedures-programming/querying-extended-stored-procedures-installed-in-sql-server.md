---
title: "查询扩展安装在 SQL Server 中的存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d17f27bf2d9822886c022103fae5834d8b4fddc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>查询在 SQL Server 中安装的扩展存储过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]经过身份验证的用户可以显示当前定义的扩展存储的过程和通过运行所属的 DLL 复制到其中的每个名称**sp_helpextendedproc**系统过程。 例如，下面的示例将返回到 DLL **xp_hello**所属：  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 如果**sp_helpextendedproc**执行而无需指定将显示扩展存储的过程、 所有扩展的存储的过程和与其 Dll。  
  
> [!IMPORTANT]  
>  将仅为那些登录用户拥有或具有权限的扩展存储过程返回信息。 只有的成员**sysadmin**固定的服务器角色和**db_owner**， **db_securityadmin**，和**db_ddladmin**固定的数据库角色可以查看所有扩展存储过程的信息。  
  
## <a name="see-also"></a>另请参阅  
 [sp_helpextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
