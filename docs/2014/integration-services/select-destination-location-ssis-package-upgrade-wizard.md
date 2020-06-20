---
title: 选择目标位置（SSIS 包升级向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c397e1e174703b40a7bada8ed6fe42675a0c9c24
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963817"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>选择目标位置（SSIS 包升级向导）
  使用 **“选择目标位置”** 页可以指定要将升级包保存到的目标位置。  
  
> [!NOTE]  
>  仅当通过 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示符运行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包升级向导时，此页才可用。  
  
 **运行 SSIS 包升级向导**  
  
-   [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>静态选项  
 **保存到源位置**  
 将升级的包保存到在向导的“选择源位置”**** 页上指定的位置。  
  
 如果原始包存储在文件系统中，并且您希望向导备份这些包，请选择 **“保存到源位置”** 选项。 有关详细信息，请参阅 [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
 **选择新的目标位置**  
 将升级的包保存到此页上指定的目标位置。  
  
 **包源**  
 指定存储升级包的位置。 此选项具有下表所列的值。  
  
|值|说明|  
|-----------|-----------------|  
|**文件系统**|指示将升级的包将保存到本地计算机上的文件夹中。|  
|**SSIS 包存储区**|指示升级的包将保存到 Integration Services 包存储区中。 包存储区由一组 Integration Services 服务管理的文件系统文件夹组成。 有关详细信息，请参阅[包管理（SSIS 服务）](service/package-management-ssis-service.md)。<br /><br /> 选择此值将显示相应的动态选项 **“包源”** 。|  
|**Microsoft SQL Server**|指示升级的包将保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的现有实例中。<br /><br /> 选择此值将显示相应的动态选项 **“包源”** 。|  
  
 **文件夹**  
 键入要保存升级包的文件夹的名称，或单击“浏览”**** 找到该文件夹。  
  
 **浏览**  
 浏览找到将保存已升级包的文件夹。  
  
## <a name="package-source-dynamic-options"></a>包源动态选项  
  
### <a name="package-source--ssis-package-store"></a>包源 = SSIS 包存储区  
 **Server**  
 键入要保存升级包的服务器的名称，或在列表中选择服务器。  
  
### <a name="package-source--microsoft-sql-server"></a>包源 = Microsoft SQL Server  
 **Server**  
 键入要保存升级包的服务器的名称，或在列表中选择此服务器。  
  
 **使用 Windows 身份验证**  
 选择此选项可以使用 Windows 身份验证连接到服务器。  
  
 **使用 SQL Server 身份验证**  
 选择此选项可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到服务器。 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 键入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到服务器时使用的用户名。  
  
 **密码**  
 键入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到服务器时使用的密码。  
  
## <a name="see-also"></a>另请参阅  
 [升级 Integration Services 包](install-windows/upgrade-integration-services-packages.md)  
  
  
