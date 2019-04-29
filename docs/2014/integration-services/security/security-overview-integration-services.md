---
title: 安全性概述 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2e86fff86e24668e7fe6382545e024bed1a4025
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62927052"
---
# <a name="security-overview-integration-services"></a>安全性概述 (Integration Services)
   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的安全性包含多层，这些层提供了丰富灵活的安全环境。 这些安全层使用数字签名、包属性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库角色和操作系统权限。 其中的大部分安全功能属于标识和访问控制类别。  
  
## <a name="identity-features"></a>标识功能  
 通过在包中实现标识功能，可达到以下目的：  
  
 **确保只打开和运行来自可信源的包**。  
  
 为了确保只打开和运行来自可信源的包，必须首先标识包的源。 可以通过使用证书对包进行签名来标识源。 然后，在打开或运行包时，可以让 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 检查数字签名是否存在以及数字签名的有效性。 有关详细信息，请参阅 [使用数字签名标识包的源](identify-the-source-of-packages-with-digital-signatures.md)。  
  
## <a name="access-control-features"></a>访问控制功能  
 通过在包中实现标识功能，可达到以下目的：  
  
 **确保只由授权用户打开和运行包**。  
  
 为了确保只由授权用户打开和运行包，必须控制对以下信息的访问：  
  
-   控制对包的内容（特别是敏感数据）的访问。  
  
-   控制对存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的包和包配置的访问。  
  
-   控制对存储在文件系统中的包和相关文件（如配置、日志和检查点文件）的访问。  
  
-   控制对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务和该服务显示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的包的信息的访问。  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>控制对包内容的访问  
 为了帮助限制对包内容的访问，可以通过设置包的 ProtectionLevel 属性来对包进行加密。 可以将此属性设置为包所需的保护级别。 例如，在组开发环境中，可以使用一个只有处理该包的组成员才知道的密码来加密包。  
  
 设置包的 ProtectionLevel 属性时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动检测敏感属性，并根据指定的包保护级别处理这些属性。 例如，将包的 ProtectionLevel 属性设置为使用密码加密敏感信息的级别。 对于此包， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动加密所有敏感属性的值，并且不会在未提供正确密码的情况下显示相应的数据。  
  
 通常，如果属性包含如密码或连接字符串这样的信息或属性对应变量或任务生成的 XML 节点， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会将这些属性标识为敏感。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 认为属性是否敏感，主要取决于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件（连接管理器或任务）的开发人员是否将该属性指定为敏感。 用户不能向被视为敏感的属性列表添加属性，也不能从该列表删除属性。如果您编写自定义任务、连接管理器或数据流组件，则可以指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 应该将哪些属性视为敏感属性。  
  
 有关详细信息，请参阅 [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md)。  
  
### <a name="controlling-access-to-packages"></a>控制对包的访问  
 您可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 msdb 数据库中，也可以作为 XML 文件保存到文件系统中，文件扩展名为 .dtsx。 有关详细信息，请参阅 [保存包](../save-packages.md)。  
  
#### <a name="saving-packages-to-the-msdb-database"></a>将包保存到 msdb 数据库  
 将包保存到 msdb 数据库有助于提供服务器级、数据库级和表级的安全性。 在 msdb 数据库中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包将存储在 sysssispackages 表中。 由于包保存到 msdb 数据库的 sysssispackages 和 sysdtspackages 表中，因此在您备份 msdb 数据库时将自动备份这些包。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以通过应用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据库级别的角色，保护 msdb 数据库中存储的包。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括三个用于控制对包访问的固定数据库级别的角色：db_ssisadmin、db_ssisltduser、和 db_ssisoperator。 每个包都可以有关联的读取者角色和写入者角色。 还可以定义要在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中使用的自定义数据库级别的角色。 只能对保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 msdb 数据库中的包实现角色。 有关详细信息，请参阅 [Integration Services Roles（SSIS 服务）](integration-services-roles-ssis-service.md)。  
  
#### <a name="saving-packages-to-the-file-system"></a>将包保存到文件系统  
 如果将包存储到文件系统而不是 msdb 数据库中，请确保包文件和包含包文件的文件夹的安全。  
  
### <a name="controlling-access-to-files-used-by-packages"></a>控制对包使用的文件的访问  
 已配置为使用配置、检查点和日志记录的包所生成的信息将存储在包的外部。 这些信息可能是敏感信息，应该加以保护。 检查点文件只能保存到文件系统中，但配置和日志可以保存到文件系统中，也可以保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的表中。 保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的配置和日志受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性的保护，但是写入文件系统的信息需要额外的安全保护措施。  
  
 有关详细信息，请参阅 [访问包使用的文件](../access-to-files-used-by-packages.md)。  
  
#### <a name="storing-package-configurations-securely"></a>安全地存储包配置  
 包配置可以保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表中，也可以保存到文件系统。  
  
 配置可以保存到任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，而不仅仅是 msdb 数据库。 因此，您可以指定要作为包配置存储库的数据库。 您还可以指定将包含这些配置的表的名称， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动创建具有正确结构的表。 通过将配置保存到表中可以提供服务器级、数据库级和表级的安全性。 此外，备份数据库时，会自动备份保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的配置。  
  
 如果将配置存储到文件系统而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，请确保包含包配置文件的文件夹的安全。  
  
 有关配置的详细信息，请参阅 [Package Configurations](../package-configurations.md)。  
  
### <a name="controlling-access-to-the-integration-services-service"></a>控制对 Integration Services 服务的访问  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务列出所存储的包。 若要防止未经授权的用户查看有关存储在本地和远程计算机上的包的信息，从而获取私有信息，请限制对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的计算机的访问。  
  
 有关详细信息，请参阅 [访问 Integration Services 服务](../access-to-the-integration-services-service.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 下面的列表包含一些链接，这些链接指向的主题说明如何执行与安全性相关的某些任务。  
  
-   [创建用户定义的角色](../create-a-user-defined-role.md)  
  
-   [将读取者角色和写入者角色分配给包](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [通过设置注册表值实现签名策略](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [使用数字证书对包签名](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [设置或更改包的保护级别](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
