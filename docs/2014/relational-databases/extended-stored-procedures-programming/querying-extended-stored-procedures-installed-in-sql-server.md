---
title: 查询扩展 SQL Server 中安装的存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f8f8616fe8b5a6c06a8492fc713e4e93004d0dad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057267"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>查询在 SQL Server 中安装的扩展存储过程
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 一个[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证的用户可以显示当前定义的扩展存储的过程和通过运行所属的 DLL 复制到其中的每个名称**sp_helpextendedproc**系统过程。 例如，下面的示例将返回到的 DLL **xp_hello**属于：  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 如果**sp_helpextendedproc**无需指定将显示扩展存储的过程、 所有扩展存储的过程和其 Dll 执行。  
  
> [!IMPORTANT]  
>  将仅为那些登录用户拥有或具有权限的扩展存储过程返回信息。 只有的成员**sysadmin**固定的服务器角色和**db_owner**， **db_securityadmin**，以及**db_ddladmin**固定的数据库角色可以查看所有扩展存储过程的信息。  
  
## <a name="see-also"></a>请参阅  
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
