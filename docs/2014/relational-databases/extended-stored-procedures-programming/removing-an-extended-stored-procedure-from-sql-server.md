---
title: 删除扩展存储过程从 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 19149de4fb5a0e62886006b620375bda5b25c9b2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227792"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>从 SQL Server 中删除扩展存储过程
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 若要在用户定义的扩展存储过程 DLL，删除每个扩展存储的过程函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统管理员必须运行**sp_dropextendedproc**系统存储过程中，指定的名称函数，并在其中该函数的 DLL 的名称。 例如，此命令将删除该函数**xp_hello**，从名为 xp_hello.dll 的 DLL 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**不会删除系统扩展存储的过程。 相反，系统管理员应拒绝针对扩展存储过程的 EXECUTE 权限**公共**角色。  
  
## <a name="see-also"></a>请参阅  
 [sp_dropextendedproc (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
