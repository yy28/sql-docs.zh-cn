---
title: 选择要配置的服务器（配置数据库镜像安全向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24e31e60f29970ca1d3a73d3a215447e9dd325bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62807233"
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>选择要配置的服务器（配置数据库镜像安全向导）
  使用此页可以指定当前要配置的服务器实例。 必须至少选择一个服务器实例，才能继续本向导。  
  
 如果清除了某个服务器实例的复选框，向导将不会对该实例做任何更改。 但是，向导会要求您输入该实例的有关信息，并将此信息保存在其他服务器实例的配置中。 例如，如果清除了见证服务器实例的复选框，向导会要求您输入见证服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户，因为必须创建该帐户的登录名，作为安全配置的一部分保存在主体和镜像服务器实例中。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **主体服务器实例**  
 选择该选项可以配置主体服务器的安全性。  
  
 **镜像服务器实例**  
 选择该选项可以配置镜像服务器的安全性。  
  
 **见证服务器实例**  
 选择该选项可以配置见证服务器（如果存在）的安全性。  
  
## <a name="see-also"></a>另请参阅  
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)  
  
  
