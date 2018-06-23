---
title: 卸载扩展存储过程 DLL |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 78d3e74d7316b31143253a2c1bd7c33d08b012f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124557"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>卸载扩展存储过程 DLL
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 立即加载的 DLL 函数之一进行调用扩展存储的过程 DLL。 该 DLL 会始终保持加载状态，直到服务器关闭或者系统管理员使用 DBCC 语句将其卸载。 例如，此命令卸载**xp_hello.dll**，允许系统管理员联系，以将此文件的较新版本复制到目录，而无需关闭服务器：  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>请参阅  
 [DBCC dll 名称&#40;免费&#41; &#40;Transact SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
