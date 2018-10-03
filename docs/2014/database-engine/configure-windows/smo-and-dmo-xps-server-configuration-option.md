---
title: “SMO 和 DMO XP”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a356db3b34db86b7b71810dcb0d030580183c879
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055927"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO 和 DMO XP 服务器配置选项
  使用 SMO 和 DMO XP 选项可以在此服务器上启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 扩展存储过程。  
  
 请注意，从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，DMO 已从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中删除。  
  
 下表中列出了该选项的可能值：  
  
|ReplTest1|含义|  
|-----------|-------------|  
|0|SMO XP 不可用。|  
|1|SMO XP 可用。 这是默认设置。|  
  
 此设置将立即生效。  
  
## <a name="examples"></a>示例  
 以下示例启用了 SMO 扩展存储过程。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 管理对象 (SMO) 编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
