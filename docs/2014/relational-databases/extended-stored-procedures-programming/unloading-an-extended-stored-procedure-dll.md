---
title: 卸载扩展存储过程 DLL |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 2772c8d6470f9ad6eb5e8b7cadb6dedd136bd48b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803919"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>卸载扩展存储过程 DLL
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 立即加载到该 DLL 的函数之一进行调用扩展存储的过程 DLL。 该 DLL 会始终保持加载状态，直到服务器关闭或者系统管理员使用 DBCC 语句将其卸载。 例如，此命令将卸载**xp_hello.dll**，允许系统管理员联系，以将此文件的较新版本复制到目录，而无需关闭服务器：  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>请参阅  
 [DBCC dllname&#40;免费&#41; &#40;TRANSACT-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
