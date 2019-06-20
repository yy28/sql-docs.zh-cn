---
title: 创建数据库向导（Master Data Services 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a808883b706700bb28888e4d66b8aa64bf1c7ee2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484531"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>创建数据库向导（主数据服务配置管理器）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  使用 **“创建数据库”** 向导可以创建 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。  
  
## <a name="database-server"></a>数据库服务器  
 指定用于连接到承载 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 数据库的本地或远程 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例的信息。 若要连接到某一远程实例，必须为远程连接启用该实例。  
  
|控件名称|Description|  
|------------------|-----------------|  
|**SQL Server 实例**|指定要承载 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例的名称。 该实例可以是本地或远程计算机上的默认实例或命名实例。 通过键入以下内容指定信息：<br /><br /> 键入一个句点 (.)，可以连接到本地计算机上的默认实例。<br /><br /> 键入服务器名或 IP 地址，可以连接到指定的本地或远程计算机上的默认实例。<br /><br /> 键入服务器名或 IP 地址以及实例名称，可以连接到指定的本地或远程计算机上的命名实例。 以 server_name  \\instance_name  格式指定此信息。|  
|**身份验证类型**|选择在连接到指定的 SQL Server 实例时要使用的身份验证的类型。 用于连接的凭据必须是指定的 **实例的** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务器角色的成员。 有关 sysadmin 角色的详细信息，请参阅 [服务器级别角色](../relational-databases/security/authentication-access/server-level-roles.md)。<br /><br /> 身份验证类型包括：<br /><br /> **当前用户 - 集成安全性**：通过使用当前 Windows 用户帐户的凭据，使用集成 Windows 身份验证进行连接。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 使用登录到计算机并打开了该应用程序的用户的 Windows 凭据。 您不能在应用程序中指定其他 Windows 凭据。 如果您想要使用其他 Windows 凭据进行连接，则必须作为该用户登录到计算机，然后打开 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。<br /><br /> **SQL Server 帐户**：使用 SQL Server 帐户进行连接。 在您选择此选项后， **“用户名”** 和 **“密码”** 字段将启用，并且您必须为指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帐户指定凭据。|  
|**用户名**|指定将用于连接到指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的用户帐户的名称。 该帐户必须是指定的 **实例上** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 角色的成员。<br /><br /> “身份验证类型”为“当前用户 - 集成安全性”时，“用户名”框为只读，并且它显示登录到计算机的 Windows 用户帐户的名称    。<br /><br /> 在 **“身份验证类型”** 为 **“SQL Server 帐户”** 时， **“用户名”** 框将启用，并且您必须为指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帐户指定凭据。|  
|**“密码”**|指定与用户帐户关联的密码：<br /><br /> “身份验证类型”为“当前用户 - 集成安全性”时，“密码”框为只读，并且使用指定 Windows 用户帐户的凭据进行连接    。<br /><br /> 在 **“身份验证类型”** 为 **“SQL Server 帐户”** 时， **“密码”** 框将启用，并且您必须指定与指定的用户帐户相关联的密码。|  
|**测试连接**|验证指定的用户帐户是否可以连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例以及该帐户是否有权为该实例创建 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。 如果您没有单击 **“测试连接”** ，则在您单击 **“下一步”** 时将测试该连接。|  
  
## <a name="database"></a>“数据库”  
 为新数据库指定数据库名称和排序规则选项。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的排序规则可为你的数据提供排序规则、区分大小写属性和区分重音属性。 用于 char 和 varchar 等字符数据类型的排序规则规定可表示该数据类型的代码页和对应字符。 有关数据库排序规则的详细信息，请参阅 [排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。  
  
|控件名称|Description|  
|------------------|-----------------|  
|**数据库名称**|指定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的名称。|  
|**SQL Server 默认排序规则**|选择此项可为新数据库使用指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的当前数据库排序规则设置。|  
|**Windows 排序规则**|指定要用于新数据库的 Windows 排序规则设置。 Windows 排序规则根据关联的 Windows 区域设置来定义字符数据的存储规则。 有关 Windows 排序规则和关联选项的详细信息，请参阅 [Windows 排序规则名称 (Transact-SQL)](../t-sql/statements/windows-collation-name-transact-sql.md)。<br /><br /> 注意：只有在取消选中“SQL Server 默认排序规则”框后，“Windows 排序规则”列表和关联选项才启用   。|  
  
## <a name="administrator-account"></a>管理员帐户  
  
|控件名称|Description|  
|------------------|-----------------|  
|**“用户名”**|为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]指定默认超级用户。 超级用户有权访问所有功能区域，并且可以添加、删除和更新所有模型。 有关超级用户权限和 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中其他类型的管理员信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。|  
  
## <a name="summary"></a>总结  
 显示所选选项的摘要。 查看您的选择，然后单击 **“下一步”** 以便使用指定的设置开始创建数据库。  
  
## <a name="progress-and-finish"></a>进度和完成  
 显示创建进程的进度。 在创建了数据库后，单击 **“完成”** 以关闭数据库向导并返回到 **“数据库”** 页。 新的数据库将被选择，并且您可以查看和修改其系统设置。  
  
## <a name="see-also"></a>请参阅  
 [“数据库配置”页（Master Data Services 配置管理器）](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)[数据库要求 &#40;Master Data Services&#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
