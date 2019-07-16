---
title: 删除扩展存储过程从 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
ms.openlocfilehash: f69de90386263df8b2be4638e257dcf58cf5dad7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064301"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>从 SQL Server 中删除扩展存储过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 若要在用户定义的扩展存储过程 DLL，删除每个扩展存储的过程函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统管理员必须运行**sp_dropextendedproc**系统存储过程中，指定的名称函数，并在其中该函数的 DLL 的名称。 例如，此命令将删除该函数**xp_hello**，从名为 xp_hello.dll 的 DLL 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**不会删除系统扩展存储的过程。 相反，系统管理员应拒绝针对扩展存储过程的 EXECUTE 权限**公共**角色。  
  
## <a name="see-also"></a>请参阅  
 [sp_dropextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
