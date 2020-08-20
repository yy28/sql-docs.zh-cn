---
description: 查询在 SQL Server 中安装的扩展存储过程
title: 查询扩展存储过程
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: edd5bb4fe5284552642a838ea2b5dcafef601061
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460809"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>查询在 SQL Server 中安装的扩展存储过程
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经过身份验证的用户可以通过运行**sp_helpextendedproc**系统过程来显示当前定义的扩展存储过程和每个存储过程所属的 DLL 的名称。 例如，下面的示例返回 **xp_hello** 所属的 DLL：  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 如果在不指定扩展存储过程的情况下执行 **sp_helpextendedproc** ，则将显示所有扩展存储过程及其 dll。  
  
> [!IMPORTANT]  
>  将仅为那些登录用户拥有或具有权限的扩展存储过程返回信息。 只有 **sysadmin** 固定服务器角色的成员和 **db_owner**、 **db_securityadmin**和 **db_ddladmin** 固定数据库角色的成员才能查看所有扩展存储过程的信息。  
  
## <a name="see-also"></a>另请参阅  
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
