---
title: 托管实例上的主机数据库 |Microsoft Docs
description: 介绍如何在托管实例上配置 MDS 数据库。
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0081ea193452e4e92938051bc7b4a40bc8631eaa
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155382"
---
# <a name="host-database-on-managed-instance"></a>托管实例上的主机数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本文介绍如何在托管实例上配置 MDS 数据库。
  
## <a name="preparation"></a>准备

我们需要在准备中完成以下步骤。
- 完成托管实例的创建和配置。 包括虚拟网络和点到站点 VPN。
- 完成 web 应用程序计算机配置。
  - 包括安装点到站点 VPN。
  - 安装角色和功能。

**数据库端:**

1. 创建 Azure SQL 数据库托管实例包括虚拟网络。 [快速入门：创建 Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. 配置点到站点连接。 [使用本机 Azure 证书身份验证配置与 VNet 的点到站点连接:Azure 门户](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. 配置 SQL 数据库托管实例 Azure Active Directory 身份验证。 [通过 SQL 配置和管理 Azure Active Directory 身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**Web 应用程序计算机端:**

1. 安装点到站点连接证书和 VPN 以确保计算机可以访问 SQL 数据库托管实例。 [使用本机 Azure 证书身份验证配置与 VNet 的点到站点连接:Azure 门户](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. 安装角色和功能。 以下功能是必需的。

- 作用

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- 功能：

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>安装和配置[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web 应用程序

需要完成以下步骤来安装和配置[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]。

1. 安装 SQL Server 2019 包括[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]功能。
2. 在管理实例上创建数据库。[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]
3. 为[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]创建和配置 web 应用程序。
  
**安装 SQL Server 2019**

使用 SQL Server 安装程序安装向导或命令提示符安装[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]。

1. 双击 Setup.exe，然后按照安装向导中的步骤进行操作。

2. 在[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] "共享功能" 下的 "功能选择" 页上选择。
将安装 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]、程序集、Windows PowerShell 管理单元以及 Web 应用程序和服务的文件夹和文件。

    ![mds-SQLServer2019-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "mds-SQLServer2019-MI_SQLFeatureSelection")  

**设置数据库和网站**

1. 连接 Azure 虚拟网络, 以确保可以连接到托管实例。

    ![mds-SQLServer2019-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "mds-SQLServer2019-MI_P2SVPNConnect")  

2. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]启动。 然后单击左窗格中的 "**数据库配置**"。

3. 单击 "**创建数据库**", 然后在 "**创建数据库**向导" 中单击 "下一步"。

4. 在 "**数据库服务器**" 页上, 填写**SQL Server 实例**并选择 "**身份验证类型**", 然后单击 "**测试连接**" 以确认可以使用身份验证类型的凭据连接到数据库。选择. 单击“下一步”。

   > [!NOTE]
   > - 托管实例的 SQL Server 实例, 如 "xxxxxxx.xxxxxxx.database.windows.net"
   > - 对于托管实例, 我们支持 **"SQL Server 帐户"** 和 **"当前用户– Active Directory 集成"** 身份验证类型。
   > - 选择 "**当前用户– Active Directory 集成**" 作为 "身份验证类型" 时, "**用户名**" 框为只读, 并显示登录到计算机的 Windows 用户帐户的名称。 如果在 Azure 虚拟机 ( [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] vm) 上运行 SQL Server 2019, 则 "**用户名**" 框将显示 vm 上的本地管理员帐户的 vm 名称和用户名。

    请确保身份验证包含托管实例的 **"sysadmin"** 规则。
![mds-SQLServer2019-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "mds-SQLServer2019-MI_CreateDBConnect")  

5. 在“数据库名称”字段中键入名称。 （可选）若要选择 Windows 排序规则，请清除“SQL Server 默认排序规则”复选框，单击一个或多个可用选项，如“区分大小写”。 单击“下一步”。

    ![mds-SQLServer2019-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "mds-SQLServer2019-MI_CreatedDBName")  

6. 在 "**用户名**" 字段中, 指定将成为默认超级用户[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]的用户的 Windows 帐户。 超级用户有权访问所有功能区域，并且可以添加、删除和更新所有模型。

    ![mds-SQLServer2019-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "mds-SQLServer2019-MI_createDBUserName")

7. 单击“下一步”查看 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 数据库的设置摘要，然后再次单击“下一步”创建数据库。 出现“进度和完成”页。

8. 创建和配置数据库后，单击“完成”。

    有关 "**创建数据库向导**" 中的设置的详细信息, 请参阅[创建&#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]数据库&#41;向导 Configuration Manager](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)。

9. 在的 "**数据库配置**" 页[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]上, 单击 "**选择数据库**"。

10. 单击 "**连接**", [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]选择你在步骤8中创建的数据库, 然后单击 **"确定"** 。

    ![mds-SQLServer2019-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-MI_connectDBName")

11. 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中，单击左窗格中的“Web 配置”。

12. 在“网站”列表框中，单击“默认网站”，然后单击“创建”以创建 Web 应用程序。
![mds-SQLServer2019-WebConfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "mds-SQLServer2019-MI_WebConfiguration")

   > [!NOTE] 
   > 选择“默认网站”时，必须创建一个 Web 应用程序。 如果在列表框中选择“创建新网站”，将自动创建应用程序。

    

13. 在 "**应用程序池**" 部分中, 输入其他用户名, 输入密码, 然后单击 "确定"。
![mds-SQLServer2019-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "mds-SQLServer2019-MI_CreateWebApplication")

   > [!NOTE]
   > 你需要确保用户可以使用你刚创建的 Active Directory 集成身份验证来访问数据库。 或者, 稍后需要更改 web.config 中的连接。

    

14. 有关 "**创建 web 应用程序**" 对话框的详细信息, 请参阅 "[创建 web &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]应用&#41;程序" 对话框 Configuration Manager](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)。

15. 在 "web**应用程序**" 框中的 " **web 配置**" 页上, 单击您创建的应用程序, 然后单击 "**将应用程序与数据库关联**" 部分中的 "**选择**"。

16. 单击“连接”，选择想要与 Web 应用程序相关联的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 数据库，然后单击“确定”。

    你已经完成了网站的设置。 " **Web 配置**" 页现在会显示所选网站、所创建的 Web 应用程序[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]以及与该应用程序关联的数据库。

    ![mds-SQLServer2019-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "mds-SQLServer2019-MI_WebConfigSelectDB")

17. 单击 **“应用”** 。 显示“配置完成”消息框。 在消息框中单击“确定”，启动 Web 应用程序。 网站地址为 http://server "名称/web 应用程序/"。

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>用于在 Web 应用程序上连接托管实例数据库的其他身份验证类型

我们可以在 C:\Program Files\Microsoft SQL Server\150\Master Data services\webapplication。下获取 web.config 文件。 我们可以修改 connectionString 以更改其他身份验证类型以连接托管实例数据库。

默认的身份验证类型为 "**Active Directory 集成**", 以下是示例连接字符串。

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

我们还支持 Active Directory 密码身份验证和 SQL Server 身份验证, 以下是示例连接字符串。

Active Directory 密码身份验证

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

SQL Server 身份验证

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>升级[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]和数据库版本

**升级[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

安装 SQL Server 2019**累积更新**, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]将自动更新。

**升级数据库版本**

如果在安装 SQL Server 2019**累积更新**后收到 "客户端版本与数据库版本不兼容" 的问题, 则需要升级数据库版本。

![mds-SQLServer2019-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "mds-SQLServer2019-MI_UpgradeDBPage")

1. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]启动。 然后单击左窗格中的 "**数据库配置**"。

2. 在的 "**数据库配置**" 页[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]上, 单击 "**选择数据库**"。

3. 单击 "**连接**", [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]选择你为 web 应用程序关联的数据库, 然后单击 **"确定"** 。

    ![mds-SQLServer2019-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "mds-SQLServer2019-MI_ConnectDBName")

4. 单击 "**升级数据库 ...** " 鼠标

    ![mds-SQLServer2019-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "mds-SQLServer2019-MI_SelectUpgradeDB")

5. 在升级数据库向导的 "**欢迎使用**" 页上, 单击 "**下一步**" 按钮, 然后单击 "**升级评审**"

    ![mds-SQLServer2019-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "mds-SQLServer2019-MI_UpgradeDBWizard")

6. 完成所有任务后, 单击 "**完成**" 按钮。

## <a name="see-also"></a>请参阅

 [Master Data Services 数据库](../master-data-services/master-data-services-database.md)[主数据管理器 Web 应用程序](../master-data-services/master-data-manager-web-application.md)"[数据库配置&#40;"&#41;页 Master Data Services 配置管理器](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)[Master Data Services &#40;MDS&#41;中的新增功能](../master-data-services/what-s-new-in-master-data-services-mds.md)
