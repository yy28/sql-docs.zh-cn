---
title: 包括见证服务器（配置数据库镜像安全向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f588b8a4305f44eceb8a8f6ab351bc940fbfef5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754943"
---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>包括见证服务器（配置数据库镜像安全向导）
  使用此页可以指定是否要将见证服务器包括在数据库镜像的安全配置中。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **是**  
 单击此项可将见证服务器实例包括在安全配置中。 对于具有自动故障转移的高安全性模式，见证服务器是必需的，因为如果主体服务器实例失败，见证服务器将提供到镜像服务器实例的自动故障转移。  
  
 **是**  
 单击此项可在不包括见证服务器的情况下配置安全性。  
  
## <a name="see-also"></a>请参阅  
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)   
 [数据库镜像见证服务器](database-mirroring-witness.md)  
  
  
