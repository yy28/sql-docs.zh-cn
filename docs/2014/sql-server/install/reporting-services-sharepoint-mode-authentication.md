---
title: Reporting Services SharePoint 模式身份验证 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 42a05beda30c678f97740a536e6b50530010bff1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125261"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services SharePoint 模式身份验证
  使用   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页可以指定在当前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中使用的服务帐户的凭据。 这些凭据将用来创建新的 SharePoint 应用程序池。 此外，还将创建一个新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服务应用程序。 客户端应用程序名称将包含前一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例的名称。  
  
## <a name="options"></a>“常规”  
  
-   **“SSRS 应用程序池帐户名称:”** 选项是只读的。 系统将自动使用来自您正在升级的现有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中的当前值填充此值。  
  
-   如果应用程序池帐户不需要密码，则将禁用 **“SSRS 应用程序池帐户密码:”** 选项。 例如，“NT Authority\NetworkSerivce”。 如果应用程序池帐户的确需要密码，仅当您键入正确的密码，才能继续进行升级。  
  
 有关详细信息，请参阅[升级和迁移 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628) (http://go.microsoft.com/fwlink/?LinkID=245628)。  
  
## <a name="see-also"></a>请参阅  
 [升级和迁移 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628)  
  
  