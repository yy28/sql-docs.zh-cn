---
title: 删除扩展存储过程从 SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dc3d3c686c4f3d0f81dc2f2bb17eb3ba29090319
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>从 SQL Server 中删除扩展存储过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 若要在用户定义扩展的存储过程 DLL，删除每个扩展存储的过程函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统管理员必须运行**sp_dropextendedproc**系统存储过程中，指定的名称函数和该函数所在的 DLL 的名称。 例如，此命令将删除该函数**xp_hello**为位于通过名为 xp_hello.dll，DLL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**不删除扩展存储的过程的系统。 相反，系统管理员应拒绝对扩展存储过程的 EXECUTE 权限**公共**角色。  
  
## <a name="see-also"></a>另请参阅  
 [sp_dropextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
