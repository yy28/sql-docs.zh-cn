---
description: 卸载扩展存储过程 DLL
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
ms.openlocfilehash: f409b15fe8212ca3d5ce25334a0241eb38feea9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408783"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>卸载扩展存储过程 DLL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]调用 dll 的一项函数后，立即加载扩展存储过程 DLL。 该 DLL 会始终保持加载状态，直到服务器关闭或者系统管理员使用 DBCC 语句将其卸载。 例如，此命令卸载 **xp_hello.dll**，允许系统管理员将此文件的较新版本复制到目录而不关闭服务器：  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>另请参阅  
 [DBCC dllname &#40;免费&#41; &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
