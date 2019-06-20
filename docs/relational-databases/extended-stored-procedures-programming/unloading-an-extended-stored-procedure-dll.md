---
title: 卸载扩展存储过程 DLL |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7f05ad92e5e5264801302f2f1e64c76478141d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742095"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>卸载扩展存储过程 DLL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 立即加载到该 DLL 的函数之一进行调用扩展存储的过程 DLL。 该 DLL 会始终保持加载状态，直到服务器关闭或者系统管理员使用 DBCC 语句将其卸载。 例如，此命令将卸载**xp_hello.dll**，允许系统管理员联系，以将此文件的较新版本复制到目录，而无需关闭服务器：  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>请参阅  
 [DBCC dllname &#40;FREE&#41; &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
