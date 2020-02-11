---
title: 从 SQL Server 中删除扩展存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62512022"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>从 SQL Server 中删除扩展存储过程
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 若要删除用户定义的扩展存储过程 DLL 中的每个扩展存储过程函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，系统管理员必须运行**sp_dropextendedproc**系统存储过程，并指定函数的名称和该函数所驻留的 DLL 的名称。 例如，此命令将从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中删除名为 XP_HELLO 的 dll 中的函数**xp_hello**：  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**不删除系统扩展存储过程。 相反，系统管理员应对**公共**角色拒绝对扩展存储过程的 EXECUTE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sp_dropextendedproc &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
