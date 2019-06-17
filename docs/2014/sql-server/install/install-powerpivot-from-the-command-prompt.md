---
title: 从命令提示符安装 PowerPivot |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e6da1b23bd23634e3edb8d92093cab6ce71a2783
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094562"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>从命令提示符安装 PowerPivot
  您可以从命令行运行安装程序以便安装 SQL Server PowerPivot for SharePoint。 您必须在命令中包含 `/ROLE` 参数并排除 `/FEATURES` 参数。  
  
## <a name="prerequisites"></a>先决条件  
 必须安装 SharePoint Server 2010 Enterprise Edition Service Pack 1 (SP1)。  
  
 您必须使用域帐户来设置 Analysis Services。  
  
 必须将计算机加入到 SharePoint 场所在的域中。  
  
##  <a name="Commands"></a> 基于 /ROLE 的安装选项  
 对于 PowerPivot for SharePoint 部署，用 `/ROLE` 参数代替 `/FEATURES` 参数。 有效值包括：  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 这两个角色均安装使 PowerPivot for SharePoint 能够在 SharePoint 场中运行的应用程序、配置和部署文件。 指定任何一个角色都将导致安装程序检查 SharePoint 集成所需的硬件和软件要求。  
  
 “现有场”选项假定已经存在 SharePoint 场。 新建场选项假定您将创建一个新场;它，以便您可以使用数据库引擎实例作为场的数据库服务器支持的命令行语法添加的数据库引擎实例。  
  
 与以往的版本相比，所有的服务器配置任务都作为安装后的任务来执行。 如果要自动执行安装和配置步骤，则可以使用 PowerShell 来配置服务器。 有关详细信息，请参阅[使用 Windows PowerShell 配置 PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)。  
  
## <a name="example-commands"></a>示例命令  
 下列示例说明了每个选项的用法。 示例 1 显示了`SPI_AS_ExistingFarm`。  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 示例 2 演示 `SPI_AS_NewFarm`。 请注意，它包括用于设置数据库引擎的参数。  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a> 修改命令语法  
 使用以下步骤可以修改示例命令语法。  
  
1.  将以下命令复制到记事本中：  
  
    ```  
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     `/q` 参数以不显示用户界面的静默模式运行安装程序。  
  
     如果为无人参与的安装指定了 `/IAcceptSQLServerLicenseTerms` 或 `/q` 参数，则 `/qs` 是必需的。  
  
     `/action` 参数指示安装程序执行安装。  
  
     `/role` 参数指示安装程序安装 PowerPivot for SharePoint 所需的 Analysis Services 程序和配置文件。 此角色还检测并使用现有场连接信息来访问 SharePoint 配置数据库。 此参数是必需的。 使用该参数（而非 `/features` 参数）指定要安装的组件。  
  
     `/instancename` 参数将“PowerPivot”指定为命名实例。 此值是硬编码的，因此不能更改。 出于教育目的在命令中指定该值，以便您知道该服务是如何安装的。  
  
     `/indicateprogress` 参数允许您在命令提示符窗口中监视进度。  
  
2.  `PID` 参数从命令中省略，该参数将导致安装 Evaluation 版本。 如果您想要安装 Enterprise 版本，则将 PID 添加到您的安装程序命令中并且提供有效的产品密钥。  
  
    ```  
  
    /PID=<product key for an Enterprise installation>  
  
    ```  
  
3.  替换为占位符\<域 \ 用户名 > 和\<StrongPassword > 使用有效的用户帐户和密码。  
  
     `/assvaccount`并 **/assvcpassword**参数用于配置[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]应用程序服务器上的实例。 请使用有效的帐户信息替换这些占位符。  
  
     **/Assysadminaccounts**参数必须设置为运行 SQL Server 安装程序的用户的标识。 您必须至少指定一个系统管理员。 请注意，SQL Server 安装程序不再自动将 sysadmin 权限授予内置 Administrators 组的成员。  
  
4.  删除换行符。  
  
5.  选择整个命令，然后单击**复制**编辑菜单上。  
  
6.  打开一个管理员命令提示符。 若要执行此操作，请单击**启动**，右键单击命令提示符，然后选择**以管理员身份运行**。  
  
7.  导航到包含 SQL Server 安装介质的驱动器或共享文件夹。  
  
8.  将修正后的命令粘贴到命令行中。 若要执行此操作，单击命令提示符窗口的左上角中的图标，指向**编辑**，然后单击**粘贴**。  
  
9. 按**Enter**运行命令。 等待安装程序完成。 您可以在命令提示符窗口中监视安装程序的进度。  
  
10. 若要验证安装，请检查 \Program Files\SQL Server\120\Setup Bootstrap\Log 处的 summary.txt 文件。 如果服务器成功安装并且没有任何错误，最终的结果应显示“Passed”。  
  
11. 配置服务器。 至少您必须部署解决方案，创建服务应用程序，并为各网站集启用功能。 有关详细信息，请参阅[配置或修复 PowerPivot for SharePoint 2010 &#40;PowerPivot 配置工具&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)或[管理中心在 PowerPivot 服务器管理和配置](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
## <a name="see-also"></a>请参阅  
 [配置 PowerPivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
