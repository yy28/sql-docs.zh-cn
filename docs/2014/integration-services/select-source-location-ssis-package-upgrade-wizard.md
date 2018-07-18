---
title: 选择源位置 （SSIS 包升级向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
caps.latest.revision: 18
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2794712f3817b3cf4d63aac7451a817cf55338b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266923"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>选择源位置（SSIS 包升级向导）
  使用 **“选择源位置”** 页可指定从中升级包的源。  
  
> [!NOTE]  
>  仅当通过 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示符运行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包升级向导时，此页才可用。  
  
 **运行 SSIS 包升级向导**  
  
-   [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>静态选项  
 **包源**  
 选择包含要升级包的存储位置。 此选项具有下表所列的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**“文件系统”**|指示要升级的包位于本地计算机上的文件夹中。<br /><br /> 若要使向导在升级这些包前备份原始包，必须在文件系统中必须存储原始包。 有关详细信息，请参阅操作指南主题。|  
|**SSIS 包存储区**|指示要升级的包位于包存储区中。 包存储区由一组 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理的系统文件夹组成。 有关详细信息，请参阅[包管理（SSIS 服务）](service/package-management-ssis-service.md)。<br /><br /> 选择此值将显示相应的动态选项 **Package source** 。|  
|**Microsoft SQL Server**|指示要升级的包来自 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的现有实例。<br /><br /> 选择此值将显示相应的动态选项 **Package source** 。|  
  
 **文件夹**  
 键入要升级的包所在的文件夹名称或单击“浏览”找到该文件夹。  
  
 **“浏览”**  
 浏览找到要升级的包所在的文件夹。  
  
## <a name="package-source-dynamic-options"></a>包源动态选项  
  
### <a name="package-source--ssis-package-store"></a>包源 = SSIS 包存储区  
 **Server**  
 键入要升级的包所在的服务器的名称，或在列表中选择此服务器。  
  
### <a name="package-source--microsoft-sql-server"></a>包源 = Microsoft SQL Server  
 **Server**  
 键入要升级的包所在的服务器的名称，或从列表中选择此服务器。  
  
 **使用 Windows 身份验证**  
 选择此选项可以使用 Windows 身份验证连接到服务器。  
  
 **使用 SQL Server 身份验证**  
 选择此选项可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到服务器。 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 键入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证用于连接到服务器的用户名。  
  
 **密码**  
 键入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证用于连接到服务器的密码。  
  
## <a name="see-also"></a>请参阅  
 [升级 Integration Services 包](install-windows/upgrade-integration-services-packages.md)  
  
  
