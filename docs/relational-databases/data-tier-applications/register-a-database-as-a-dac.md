---
title: 将数据库注册为 DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.registerdacwizard.summary.f1
- sql13.swb.registerdacwizard.introduction.f1
- sql13.swb.registerdacwizard.setproperties.f1
- sql13.swb.registerdacwizard.registerdac.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c80a09793bae9691c25590b1c929a76f0da4e4b0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="register-a-database-as-a-dac"></a>将数据库注册为 DAC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用“注册数据层应用程序向导”  或 Windows PowerShell 脚本可以生成描述现有数据库中对象的数据层应用程序 (DAC) 定义，并在 **msdb** 系统数据库（**中为** master [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]）中注册 DAC 定义。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **若要升级 DAC，请使用：**[注册数据层应用程序向导](#UsingRegisterDACWizard)、[PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>开始之前  
 注册过程将创建用于定义数据库中的对象的 DAC 定义。 DAC 定义与数据库的组合构成一个 DAC 实例。 如果在数据库引擎的托管实例上将数据库注册为 DAC，则在下次将实用工具收集组从该实例发送到实用工具控制点时，已注册的 DAC 将合并到 SQL Server 实用工具中。 然后，该 DAC 将出现 **中的** “实用工具资源管理器” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **“已部署的数据层应用程序”** 节点下，并且在 **中的** 详细信息页中报告。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 只能在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更高版本的数据库上执行 DAC 注册。 如果已为数据库注册了 DAC，则无法执行 DAC 注册。 例如，如果数据库是通过部署 DAC 创建的，则无法运行 “注册数据层应用程序向导”。  
  
 如果数据库有 DAC 中不支持的对象或包含的用户，则不能注册 DAC。 有关 DAC 中支持的对象类型的详细信息，请参阅 [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)。  
  
###  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中注册 DAC 至少需要 ALTER ANY LOGIN 和数据库范围 VIEW DEFINITION 权限，对 **sys.sql_expression_dependencies**具有 SELECT 权限，且具备 **dbcreator** 固定服务器角色的成员身份。 **sysadmin** 固定服务器角色的成员或名为 **sa** 的内置 SQL Server 系统管理员帐户也可以注册 DAC。 注册在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中不包含登录名的 DAC 要求具有 **dbmanager** 或 **serveradmin** 角色的成员身份。 注册在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中包含登录名的 DAC 要求具有 **loginmanager** 或 **serveradmin** 角色的成员身份。  
  
##  <a name="UsingRegisterDACWizard"></a> 使用注册数据层应用程序向导  
 **使用向导注册 DAC**  
  
1.  在 **“对象资源管理器”**中，展开包含要注册为 DAC 的数据库的实例的节点。  
  
2.  展开 **“数据库”** 节点。  
  
3.  右键单击要注册的数据库，指向 “任务”，然后选择   
  
4.  完成向导对话框：  
  
    1.  [“简介”页](#Introduction)  
  
    2.  [“设置属性”页](#Set_properties)  
  
    3.  [“验证和摘要”页](#Summary)  
  
    4.  [“注册 DAC”页](#Register)  
  
##  <a name="Introduction"></a> “简介”页  
 此页描述用于注册数据层应用程序的各个步骤。  
  
 **不再显示此页。** - 选中该复选框可以停止在将来显示此页。  
  
 “下一步>”- 进入“设置属性”页。  
  
  “取消”- 终止向导而不注册 DAC。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
##  <a name="Set_properties"></a> “设置属性”页  
 使用此页可指定 DAC 级别的属性，如应用程序名称和版本。  
  
 **应用程序名称。** - 指定用于标识 DAC 定义的名称的字符串，该字段用数据库名称进行填充。  
  
 **版本。** - 标识 DAC 版本的数值。 该 DAC 版本用于 Visual Studio 中，以便标识开发人员正在处理的 DAC 的版本。 在部署 DAC 时，该版本存储于 **msdb** 数据库中，并且以后可以在 **中的“数据层应用程序”**[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]节点下查看。  
  
 **说明。** - 可选。 用来说明 DAC 用途的文本。 在部署 DAC 时，该描述存储于 **msdb** 数据库中，并且以后可以在 **中的“数据层应用程序”**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]节点下查看。  
  
 “<上一步”- 返回到“简介”页。  
  
 “下一步>”- 验证 DAC 是否可从数据库中的对象生成，并在“验证和摘要”页中显示结果。  
  
  “取消”- 终止向导而不注册 DAC。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
##  <a name="Summary"></a> “验证和摘要”页  
 使用此页可以查看在注册 DAC 时向导将执行的操作。 当该页验证可从数据库的对象中生成 DAC 时，它将经历三个状态。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
### <a name="retrieving-objects"></a>检索对象  
 **检索数据库和服务器对象。** - 当该向导从数据库和数据库引擎实例中检索所有所需对象时，将显示一个进度栏。  
  
 “<上一步”- 返回到“设置属性”页以便更改条目。  
  
 “下一步>”- 注册 DAC 并在“注册 DAC”页中显示结果。  
  
  “取消”- 终止向导而不注册 DAC。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
### <a name="validating-objects"></a>验证对象  
 **检查**  *SchemaName* **。** *ObjectName* **“注册数据层应用程序向导”。** - 当该向导验证所检索对象的依赖项并验证这些对象都是用于 DAC 的有效对象时，将显示一个进度栏。 SchemaName.ObjectName** 确定当前正在验证的对象。  
  
 “<上一步”- 返回到“设置属性”页以便更改条目。  
  
 “下一步>”- 注册 DAC 并在“注册 DAC”页中显示结果。  
  
  “取消”- 终止向导而不注册 DAC。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
### <a name="summary"></a>“摘要”  
 **将使用以下设置注册 DAC。** - 显示将包含在 DAC 中的属性和对象的报表。  
  
  “保存报表”- 选择此按钮可以将验证报表的副本保存到某一 HTML 文件。 默认文件夹是你 Windows 帐户的 Documents 文件夹中的 **SQL Server Management Studio\DAC Packages** 文件夹。  
  
 “<上一步”- 返回到“设置属性”页以便更改条目。  
  
 “下一步>”- 注册 DAC 并在“注册 DAC”页中显示结果。  
  
  “取消”- 终止向导而不注册 DAC。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
##  <a name="Register"></a> “注册 DAC”页  
 此页报告注册成功与否。  
  
  “注册 DAC”- 报告为注册 DAC 而执行的每个操作成功与否。 查看信息以便确定每个操作是成功还是失败。 遇到了错误的任何操作都将在 **“结果”** 列中具有一个链接。 选择该链接可以查看针对该操作的错误报告。  
  
  “保存报表”- 选择此按钮可以将注册报表保存到某一 HTML 文件。 该文件报告每个操作的状态，并且包括任何操作生成的所有错误。 默认文件夹是你 Windows 帐户的 Documents 文件夹中的 **SQL Server Management Studio\DAC Packages** 文件夹。 文件名采用 \<DACPackageName>_RegisterDACReport_yyyymmdd.html 的格式。其中，\<*DACPackageName*> 是所部署的包的名称，*yyyy* = 当前年份，*mm* = 当前月份，*dd* = 当前日期。  
  
 “完成” - 终止向导。  
  
 [使用注册数据层应用程序向导](#UsingRegisterDACWizard)  
  
##  <a name="RegisterDACPowerShell"></a> 使用 PowerShell 注册 DAC  
 **在 PowerShell 脚本中使用 Register() 方法将数据库注册为 DAC**  
  
1.  创建一个 SMO Server 对象，并且将该对象设置为包含要注册为 DAC 的数据库的实例。  
  
2.  添加一个指定数据库名称的变量。  
  
3.  指定 DAC 的元数据，如 DAC 名称、版本和说明。  
  
4.  使用上面指定的信息运行 Register 方法。  
  
### <a name="example-powershell"></a>示例 (PowerShell)  
 下面的示例将名为 MyDB 的数据库注册为 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
