---
title: 包括见证服务器（配置数据库镜像安全向导）
description: 介绍 SQL Server Management Studio (SSMS) GUI 中“配置数据库镜像安全性”向导的“包含见证服务器”页面。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9c1c3de18f4da7d6f55ad0bba5b684e21989b1e0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253561"
---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>包括见证服务器（配置数据库镜像安全向导）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此页可以指定是否要将见证服务器包括在数据库镜像的安全配置中。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **是**  
 单击此项可将见证服务器实例包括在安全配置中。 对于具有自动故障转移的高安全性模式，见证服务器是必需的，因为如果主体服务器实例失败，见证服务器将提供到镜像服务器实例的自动故障转移。  
  
 **是**  
 单击此项可在不包括见证服务器的情况下配置安全性。  
  
## <a name="see-also"></a>另请参阅  
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [数据库镜像见证服务器](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
