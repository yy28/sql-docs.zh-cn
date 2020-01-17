---
title: 配置安全向导：选择服务器
descriptoin: Describes the properties found on the the 'Choose Servers' page of the 'Configure Database Mirroring Security Wizard'.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cfb2396e97c4cceee534472c07c285aa2a8a371e
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822313"
---
# <a name="configure-database-mirroring-wizard-choose-servers-to-configure"></a>配置数据库镜像向导：选择要配置的服务器 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此页可以指定当前要配置的服务器实例。 必须至少选择一个服务器实例，才能继续本向导。  
  
 如果清除了某个服务器实例的复选框，向导将不会对该实例做任何更改。 但是，向导会要求您输入该实例的有关信息，并将此信息保存在其他服务器实例的配置中。 例如，如果清除了见证服务器实例的复选框，向导会要求您输入见证服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户，因为必须创建该帐户的登录名，作为安全配置的一部分保存在主体和镜像服务器实例中。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **主体服务器实例**  
 选择该选项可以配置主体服务器的安全性。  
  
 **镜像服务器实例**  
 选择该选项可以配置镜像服务器的安全性。  
  
 **见证服务器实例**  
 选择该选项可以配置见证服务器（如果存在）的安全性。  
  
## <a name="see-also"></a>另请参阅  
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
