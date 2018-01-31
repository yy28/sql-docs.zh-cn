---
title: "早期包部署 (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: packages
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f0a4d37996a1add0c028f9481b1dc232190a19a3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="legacy-package-deployment-ssis"></a>早期包部署 (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括一些工具和向导，它们简化了将包从开发计算机部署到生产服务器或其他计算机的过程。  
  
 包部署过程中有四个步骤：  
  
1.  第一个可选步骤是可选的，包括创建在运行时更新包元素属性的包配置。 部署包时会自动包括这些配置。  
  
2.  第二步是生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，用于创建包部署实用工具。 项目的部署实用工具包含要部署的包  
  
3.  第三步是将生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目时创建的部署文件夹复制到目标计算机中。  
  
4.  第四步是在目标计算机上运行包安装向导，以将包安装到文件系统或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  

## <a name="package-configurations"></a>包配置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供可用于在运行时更新属性值的包配置。  
  
> **注意：** 配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)。   
  
 配置是添加到已完成包中的属性/值对。 通常，在包开发期间您在包对象上创建包设置属性，然后将配置添加到包中。 当包运行时，它从配置中获取新的属性值。 例如，通过使用配置，您可以更改连接管理器的连接字符串，或者更新变量的值。  
  
 包配置具有下列优点：  
  
-   使用配置可以更轻松地将包从开发环境转移到生产环境中。 例如，配置可以更新源文件的路径，或者更改数据库或服务器的名称。  
  
-   将包部署到多台不同的服务器时，配置非常有用。 例如，用于每个已部署包的配置中的变量可以包含不同的磁盘空间，并且如果可用磁盘空间不满足此值，包将不会运行。  
  
-   配置可以使包更加灵活。 例如，配置可以更新在属性表达式中使用的变量的值。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持几种不同的存储包配置（例如 XML 文件、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的表以及环境变量和包变量）的方法。  
  
 每个配置都是一个属性/值对。 XML 配置文件和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置类型可以包括多个配置。  
  
 在创建用于安装包的包部署实用工具时将会包括这些配置。 在安装包时，可以在安装包的过程中更新配置。  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>了解在运行时如何应用包配置  
 使用 **dtexec** 命令提示实用工具 (dtexec.exe) 运行部署的包时，该实用工具将应用两次包配置。 该实用工具将在它应用在命令行上指定的选项之前和之后各应用一次包配置。  
  
 在实用工具加载和运行包时，事件的发生顺序如下：  
  
1.  **dtexec** 实用工具加载包。  
  
2.  该实用工具应用设计时在包中指定的配置，并根据在包中指定的顺序应用。 （唯一的例外是父包变量配置。 该实用工具仅应用一次这些配置，并且是在过程的后面应用。）  
  
3.  该实用工具随后应用在命令行上指定的任何选项。  
  
4.  该实用工具随后重新加载设计时在包中指定的配置，并根据在包中指定的顺序重新加载。 （同样，此规则唯一的例外是父包变量配置）。 该实用工具使用指定的任何命令行选项来重新加载配置。 因此，可能从不同位置重新加载不同值。  
  
5.  该实用程序应用父包变量配置。  
  
6.  该实用工具运行包。  
  
 **dtexec** 实用工具应用配置的方式会影响以下命令行选项：  
  
-   在运行时，可以使用 **/Connection** 或 **/Set** 选项从在设计时指定的位置之外的某个位置加载包配置。  
  
-   可以使用 **/ConfigFile** 选项加载在设计时未指定的其他配置。  
  
 但是，这些命令行选项确实存在一些限制：  
  
-   不能使用 **/Set** 或 **/Connection** 选项替代同样由配置设置的单个值。  
  
-   不能使用 **/ConfigFile** 选项加载用来替换在设计时指定的配置的配置。  
  
 有关这些选项以及其在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 和早期版本中的行为的区别的详细信息，请参阅 [SQL Server 2016 中 Integration Services 功能的行为更改](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)。  
  
### <a name="package-configuration-types"></a>包配置类型  
 下表介绍了包配置的类型。  
  
|类型|Description|  
|----------|-----------------|  
|XML 配置文件|XML 文件包含配置。 XML 文件可以包括多个配置。|  
|环境变量|环境变量包含配置。|  
|注册表项|注册表项包含配置。|  
|父包变量|包中的变量包含配置。 此配置类型通常用于更新子包中的属性。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的表包含配置。 表可以包括多个配置。|  
  
#### <a name="xml-configuration-files"></a>XML 配置文件  
 如果选择 **“XML 配置文件”** 配置类型，您可以创建一个新的配置文件；重用现有文件并添加新的配置；也可以重用现有文件但覆盖现有文件的内容。  
  
 XML 配置文件包括两部分：  
  
-   包含有关配置文件信息的标题。 此元素包括的属性有该文件的创建时间和该文件的创建者的姓名等。  
  
-   包含有关每个配置的信息的配置元素。 此元素包括的特性有属性路径和属性的配置值等。  
  
 下列 XML 代码说明了 XML 配置文件的语法。 此示例显示了一个名为 `MyVar`的整数变量的 Value 属性配置。  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>注册表项  
 如果要使用注册表项存储配置，可以使用已有项或在 HKEY_CURRENT_USER 中创建新项。 使用的注册表项必须具有名为 **Value**的值。 该值可以是 DWORD 或一个字符串。  
  
 如果选择 **“注册表项”** 配置类型，请在“注册表项”框中键入注册表项的名称。 格式为 \<registry key>。 如果要使用不在 HKEY_CURRENT_USER 根目录下的注册表项，请使用 \<Registry key\registry key\\...> 格式来标识该项。 例如，若要使用 SSISPackages 中的 MyPackage 项，请键入 **SSISPackages\MyPackage**。  
  
#### <a name="sql-server"></a>SQL Server  
 如果选择 **SQL Server** 配置类型，则需指定到要存储这些配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接。 可以将配置保存到现有表，也可以在指定数据库中新建表。  
  
 下面的 SQL 语句说明了包配置向导提供的默认 CREATE TABLE 语句。  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 您为配置提供的名称就是在 **ConfigurationFilter** 列中存储的值。  
  
### <a name="direct-and-indirect-configurations"></a>直接配置和间接配置  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了直接配置和间接配置。 如果直接指定配置， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会在配置项和包对象属性之间创建直接链接。 如果源的位置不更改，则直接配置是较好的选择。 例如，如果确定包中的所有部署都使用相同的文件路径，则可以指定一个 XML 配置文件。  
  
 间接配置使用环境变量。 配置不直接指定配置设置，而是指向环境变量，环境变量又包含配置值。 如果对于包的每个部署，配置的位置都可以更改，则使用间接配置是较好的选择。  

## <a name="create-package-configurations"></a>创建包配置
  使用“包配置组织程序”对话框和包配置向导，可以创建包配置。 若要访问这些工具，请在 **中单击** “SSIS” **菜单上的** “包配置” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
  
 **说明：**
>还可以通过单击“配置”属性旁的省略号按钮，访问“包配置组织程序”。 “配置”选项出现在包的属性窗口中。  
  
>配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)。    
  
>在 **“包配置组织程序”** 对话框中，可以启用包以使用配置、添加和删除配置以及设置加载配置的首选顺序。 
 
>如果包配置按照首选顺序加载，则配置按照从 **“包配置组织程序”** 对话框中显示的列表顶部到列表底部的顺序进行加载。 但是，在运行时，包配置可能不会按照首选顺序加载。 尤其是，父包配置将在其他类型的配置之后加载。  
  
>如果多个配置设置相同的对象属性，则在运行时使用最后加载的值。  
  
 从 **“包配置组织程序”** 对话框中，可以运行包配置向导，该向导将指导您完成创建配置的步骤。 若要运行包配置向导，请在 **“包配置组织程序”** 对话框中添加新配置，或编辑现有的配置。 在向导的各页上，您可以选择配置类型，选择是直接访问配置还是使用环境变量，以及选择要在配置中保存的属性。  
  
 以下示例在包配置向导的“完成向导”页中出现变量和包时显示它们的目标属性。  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 在此示例中，配置将更新以下属性：  
  
-   用户定义变量 `TodaysDate`的 RaiseChangedEvent 属性。  
  
-   包的 MaximumErrorCount、LoggingMode 和 LocaleID 属性。  
  
-   用户定义变量 `varTableName`在“我的 SQL 任务”的作用域内的 Value 属性。  
  
 “\Package”表示根，句点 (.) 分隔用于定义配置所更新属性的路径的对象。 变量和属性的名称用括号括起。 配置中始终使用术语“包”，而与包名称无关；但是，路径中的所有其他对象都使用其用户定义名称。  
  
 在向导完成后，新的配置将添加到 **“包配置组织程序”** 对话框的配置列表中。  
  
> **注意：** 包配置向导的最后一页“完成向导”列出了配置中的目标属性。 如果希望通过使用 **dtexec** 命令提示符实用工具在运行包时更新属性，则可以通过运行包配置向导来生成表示属性路径的字符串，然后将它们复制并粘贴到命令提示符窗口中，以便用于 **dtexec**的设置选项。  
  
 下表介绍 **“包配置组织程序”** 对话框的配置列表中的各列。  
  
|“列”|Description|  
|------------|-----------------|  
|**配置名称**|配置的名称。|  
|**配置类型**|配置类型。|  
|**配置字符串**|配置的位置。 位置可以是路径、环境变量、注册表项、父包变量名或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的表。|  
|**目标对象**|其属性具有配置的对象的名称。 如果配置是 XML 配置文件，则该列为空，因为该配置可以更新多个对象。|  
|**目标属性**|属性的名称。 如果配置写入 XML 配置文件或 SQL Server 表，则列为空，因为配置可以更新多个对象。|  
  
### <a name="to-create-a-package-configuration"></a>创建包配置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，单击 **“控制流”**、 **“数据流”**、 **“事件处理程序”**或 **“包资源管理器”** 选项卡。  
  
4.  在 **SSIS** 菜单上，单击“包配置” 。  
  
5.  在 **“包配置组织程序”** 对话框中，选择 **“启用包配置”**，再单击 **“添加”**。  
  
6.  在“包配置向导”页的欢迎页上，单击 **“下一步”**。  
  
7.  在“选择配置类型”页上，指定配置类型，然后设置与该配置类型相关的属性。 有关详细信息，请参阅 [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md)。  
  
8.  在“选择要导出的属性”页上，选择要在配置中包括的包对象的属性。 如果配置类型只支持一个属性，则此向导页的标题是“选择目标属性”。 有关详细信息，请参阅 [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md)。  
  
    > **注意：** 只有 **XML 配置文件** 和 **SQL Server** 配置类型支持在一个配置中包括多个属性。  
  
9. 在“完成向导”页上，键入配置的名称，然后单击 **“完成”**。  
  
10. 查看 **“包配置组织程序”** 对话框中的配置。  
  
11. 单击 **“关闭”**。  

## <a name="package-configurations-organizer"></a>“包配置组织程序”
  可以使用 **“包配置组织程序”** 对话框启用包配置，查看当前包的配置列表以及指定加载这些配置的首选顺序。  
  
> **注意：** 配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)。    
  
 如果多个配置更新同一属性，则在配置列表中排列靠后的配置的值将代替在列表中排列靠前的配置的值。 最后加载到属性中的值是在包运行时将要使用的值。 而且，如果包使用直接配置（例如 XML 配置文件）和间接配置（例如环境变量）的组合，那么指向直接配置的位置的间接配置必须在列表中处于靠前位置。  
  
> **注意：**如果包配置按照首选顺序加载，则配置按照从“包配置组织程序”对话框中显示的列表顶部到列表底部的顺序进行加载。 但是，在运行时，包配置可能不会按照首选顺序加载。 父包配置将在其他类型的配置之后加载的情况尤其如此。  
  
 在运行时，包配置将更新包对象的属性值。 加载包时，配置中的值将替换开发包时所设置的值。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持不同的配置类型。 例如，您可以使用包含多个配置的 XML 文件或包含单个配置的环境变量。 有关详细信息，请参阅 [Package Configurations](../../integration-services/packages/package-configurations.md)。  
  
### <a name="options"></a>“常规”  
 **启用包配置**  
 选择此选项可对包使用配置。  
  
 **配置名称**  
 查看配置的名称。  
  
 **配置类型**  
 查看存储配置的位置类型。  
  
 **配置字符串**  
 查看存储配置值的位置。 该位置可以是文件路径、环境变量的名称、父级包变量的名称、注册表项或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表的名称。  
  
 **目标对象**  
 查看配置更新的对象的名称。 如果配置是 XML 配置文件或 SQL Server 表，则列为空，因为配置可以包含多个对象。  
  
 **目标属性**  
 查看配置修改的属性的名称。 如果配置类型支持多个配置，则此列为空白。  
  
 **“添加”**  
 通过使用包配置向导来添加配置。  
  
 **编辑**  
 通过重新运行包配置向导来编辑现有配置。  
  
 **删除**  
 选择一个配置，再单击“删除”。  
  
 **箭头**  
 在列表中选择一个配置，再使用向上键和向下键可将其上移或下移。 配置将按照在列表中的显示顺序来进行加载。  

## <a name="package-configuration-wizard-ui-reference"></a>包配置向导用户界面参考
  可以使用 **“包配置向导”** 创建在运行时更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包及其对象的属性的配置。 当您在 **“包配置组织程序”** 对话框中添加新配置或者修改现有配置时，将运行该向导。 若要打开 **“包配置组织程序”** 对话框，请在 **上的** SSIS **菜单中选择** “包配置” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 有关详细信息，请参阅 [创建包配置](../../integration-services/packages/create-package-configurations.md)。  
  
> **注意：** 配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)。  
  
 以下部分介绍了该向导中的各页。  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>“欢迎使用包配置向导”页  
 使用 **“SSIS 配置向导”** 可以创建在运行时更新包及其对象的属性的配置。  
  
#### <a name="options"></a>“常规”  
 **不再显示此页**  
 下次打开向导时跳过欢迎页。  
  
 **Next**  
 转到向导的下一页。  
  
### <a name="select-configuration-type-page"></a>“选择配置类型”页  
 使用 **“选择配置类型”** 页可以指定要创建的配置类型。  
  
 如果需要其他信息才能确定要使用的配置类型，则请参阅 [Package Configurations](../../integration-services/packages/package-configurations.md)。  
  
#### <a name="static-options"></a>静态选项  
 **配置类型**  
 使用下列选项选择存储配置的源的类型：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**XML 配置文件**|将配置存储为 XML 文件。 选择此值将显示 **“配置类型”**部分中的动态选项。|  
|**环境变量**|将配置存储在一个环境变量中。 选择此值将显示 **“配置类型”**部分中的动态选项。|  
|**注册表项**|将配置存储在注册表中。 选择此值将显示 **“配置类型”**部分中的动态选项。|  
|**父包变量**|将配置存储为包含该任务的包中的变量。  选择此值将显示 **“配置类型”**部分中的动态选项。|  
|**SQL Server**|将配置存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中。 选择此值将显示 **“配置类型”**部分中的动态选项。|  
  
 **Next**  
 查看向导的下一页。  
  
#### <a name="dynamic-options"></a>动态选项  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>配置类型选项 = XML 配置文件  
 **直接指定配置设置**  
 用于直接指定设置。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**配置文件名**|键入向导生成的配置文件的路径。|  
|**“浏览”**|使用 **“选择配置文件位置”** 对话框指定向导生成的配置文件的路径。 如果文件不存在，则向导将创建该文件。|  
  
 **配置位置存储在一个环境变量中**  
 用于指定存储配置的环境变量。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**环境变量**|从列表中选择环境变量。|  
  
##### <a name="configuration-type-option--environment-variable"></a>配置类型选项 = 环境变量  
 **环境变量**  
 选择包含配置信息的环境变量。  
  
##### <a name="configuration-type-option--registry-entry"></a>配置类型选项 = 注册表项  
 **直接指定配置设置**  
 用于直接指定设置。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**注册表项**|键入包含配置信息的注册表项。 格式为 \<registry key>。<br /><br /> 该注册表项必须已经存在于 HKEY_CURRENT_USER 中并且具有一个名为 Value 的值。 该值可以是 DWORD 或一个字符串。<br /><br /> 如果要使用不在 HKEY_CURRENT_USER 根目录下的注册表项，请使用 \<Registry key\registry key\\...> 格式来标识该项。|  
  
 **配置位置存储在一个环境变量中**  
 用于指定存储配置的环境变量。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**环境变量**|从列表中选择环境变量。|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>配置类型选项 = 父包变量  
 **直接指定配置设置**  
 用于直接指定设置。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**父变量**|指定父包中包含配置信息的变量。|  
  
 **配置位置存储在一个环境变量中**  
 用于指定存储配置的环境变量。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**环境变量**|从列表中选择环境变量。|  
  
##### <a name="configuration-type-options--sql-server"></a>配置类型选项 = SQL Server  
 **直接指定配置设置**  
 用于直接指定设置。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**“连接”**|从列表中选择连接，或者单击 **“新建”** 创建新连接。|  
|**配置表**|选择现有的表，或者单击 **“新建”** 编写用于创建新表的 SQL 语句。|  
|**配置筛选器**|选择现有配置名称或者键入新名称。<br /><br /> 多个 SQL Server 配置可以存储在同一个表中，而且每个配置可以包括多个配置项。<br /><br /> 此用户定义值存储在表中以标识属于特定配置的配置项|  
  
 **配置位置存储在一个环境变量中**  
 用于指定存储配置的环境变量。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**环境变量**|从列表中选择环境变量。|  
  
### <a name="select-objects-to-export-page"></a>“选择要导出的对象”页  
 使用 **“选择目标属性”** 或“选择要导出的属性”页可以指定配置包含的对象属性。 只有在选择 XML 配置类型时，才能选择多个属性。  
  
#### <a name="options"></a>“常规”  
 **对象**  
 展开包层次结构并选择要导出的属性。  
  
 **属性特性**  
 查看属性的特性。  
  
 **Next**  
 转到向导的下一页。  
  
### <a name="completing-the-wizard-page"></a>“完成向导”页  
 使用 **“完成向导”** 页可以提供配置的名称以及查看此向导用于创建配置的设置。 在向导完成之后，将显示 **“包配置组织程序”** ，其中列出了包的所有配置。  
  
#### <a name="options"></a>“常规”  
 **配置名称**  
 键入配置的名称。  
  
 **预览**  
 查看此向导用于创建配置的设置。  
  
 **“完成”**  
 创建配置并退出 **包配置向导**。  

## <a name="child"></a>在子包中使用变量和参数的值
  此过程介绍如何创建使用父变量配置类型的包配置。 通过此配置类型，从父包运行的子包可以访问父包中的变量。  
  
> [!NOTE]  
>  您还可以通过配置执行包任务将值传递给子包，以将父包变量或参数（或项目参数）映射到子包参数。 有关详细信息，请参阅 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)。  
  
 在子包中创建包配置之前，不必在父包中创建变量。 可以随时在父包中添加变量，但必须在包配置中使用准确的父变量名称。 但是，在配置可以更新的子包中必须有现成的变量，然后才能创建父变量配置。 有关添加和配置变量的详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
 父包中用于父变量配置的变量的作用域可以设置为“执行包”任务、包含任务的容器或包。 如果在包中定义了多个同名的变量，则使用在作用域中最接近“执行包”任务的变量。 最接近“执行包”任务的作用域是该任务本身。  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>向父包中添加变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含目标包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，所谓目标包是指您想将要传递给子包的变量添加到其中的包。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，若要定义变量的作用域，请执行下列操作之一：  
  
    -   若要设置包的范围，请单击 **“控制流”** 选项卡设计图面上的任何位置。  
  
    -   若要将作用域设置为“执行包”任务的父容器，请单击该容器。  
  
    -   若要将作用域设置为“执行包”任务，请单击该任务。  
  
4.  添加并配置变量。  
  
    > [!NOTE]  
    >  选择与变量将要存储的数据兼容的数据类型。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-add-a-variable-to-a-child-package"></a>向子包中添加变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，有一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目应当包含您要向其中添加父变量配置的包，请将该项目打开。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，若要设置包的作用域，请在 **“控制流”** 选项卡的设计图面上单击任何位置。  
  
4.  添加并配置变量。  
  
    > [!NOTE]  
    >  选择与变量将要存储的数据兼容的数据类型。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  

## <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  部署包的第一步是为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目创建一个部署实用工具。 部署实用工具是一个文件夹，其中包含在不同服务器上部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目中的包所需的文件。 部署实用工具是在存储 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的计算机上创建的。  
  
 通过首先配置创建部署实用工具的生成过程，然后生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，可以为该项目创建一个包部署实用工具。 在生成项目时，将自动包括项目中的所有包和包配置。 若要部署其他文件（如项目的自述文件），请将这些文件放在 **项目的** “杂项” [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 文件夹中。 当生成项目时，也会自动包括这些文件。  
  
 您可以按照不同的方式配置每个项目部署。 在生成项目和创建包部署实用工具之前，您可以设置部署实用工具的属性，自定义项目中包的部署方法。 例如，您可以指定在部署项目时是否可以更新包配置。 若要访问 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的属性，请右键单击该项目，再单击“属性”。  
  
 下表列出了部署实用工具属性。  
  
|“属性”|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|一个指定在部署过程中是否可以更新配置的值。|  
|CreateDeploymentUtility|一个指定在生成项目时是否创建包部署实用工具的值。 此属性必须为 **True** 才能创建部署实用工具。|  
|DeploymentOutputPath|部署实用工具的位置，相对于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。|  
  
 在生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目时，除了创建项目包的副本和包依赖项外，还会创建一个清单文件 \<project name>.SSISDeploymentManifest.xml，并将它们都添加到项目的 bin\Deployment 文件夹中，或添加到 DeploymentOutputPath 属性中所指定的位置。 该清单文件列出了项目中的包、包配置和所有杂项文件。  
  
 每次生成项目时将刷新部署文件夹的内容。 这意味着系统将删除所有已保存到此文件夹中但未由生成进程再次复制到该文件夹中的文件。 例如，将删除保存到部署文件夹中的包配置文件。  
  
### <a name="to-create-a-package-deployment-utility"></a>创建包部署实用工具  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含要为其创建包部署实用工具的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的解决方案。  
  
2.  右键单击该项目，再单击“属性”。  
  
3.  在“\<project name> 属性页”对话框中，单击“部署实用工具”。  
  
4.  若要在部署包时更新包配置，请将 **AllowConfigurationChanges** 设置为 **True**。  
  
5.  将 **CreateDeploymentUtility** 设置为 **True**。  
  
6.  还可以通过修改 **DeploymentOutputPath** 属性来更新部署实用工具的位置。  
  
7.  单击“确定” 。  
  
8.  在解决方案资源管理器中，右键单击该项目，再单击“生成”。  
  
9. 在 **“输出”** 窗口中查看生成进度和生成错误。  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>使用部署实用工具部署包
  如果要使用所生成的部署实用工具将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目中的包安装到与生成该工具的计算机不同的其他计算机上，则必须首先将部署文件夹复制到目标计算机上。  
  
 部署文件夹的路径是在为其创建部署实用工具的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的 DeploymentOutputPath 属性中指定的。 默认路径为 bin\Deployment，它相对于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象。 有关详细信息，请参阅 [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md)。  
  
 可以使用包安装向导安装包。 若要启动向导，在将部署文件夹复制到服务器之后，请双击部署实用工具文件。 此文件名为 \<项目名称>.SSISDeploymentManifest，可以在目标计算机上的部署文件夹找到它。  
  
> [!NOTE]  
>  如果并行安装了不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，根据你部署的包的版本，可能会遇到错误。 因为 .SSISDeploymentManifest 文件扩展名对于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的所有版本是相同的，因此可能出现此错误。 针对最近安装的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]版本双击该文件调用安装程序 (dtsinstall.exe)，它的版本可能与部署实用工具文件的版本不同。 若要解决这个问题，请从命令行运行正确的 dtsinstall.exe 版本，并且提供部署实用工具文件的路径。  
  
 包安装向导指导您完成将包安装到文件系统或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的步骤。 可以按下列方式配置安装：  
  
-   选择安装包的位置类型和位置。  
  
-   选择安装包的依赖项的位置。  
  
-   在目标服务器上安装包之后对其进行验证。  
  
 包的基于文件的依赖项始终都安装到文件系统中。 如果要将包安装到文件系统中，则依赖项也会安装到您为包所指定的文件夹中。 如果将包安装到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以指定存储基于文件的依赖项的文件夹。  
  
 如果包包括要进行修改以便在目标计算机上使用的配置，您可以使用该向导更新属性的值。  
  
 除了使用包安装向导安装包之外，还可以使用 **dtutil** 命令提示实用工具来复制和移动包。 有关详细信息，请参阅 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>将包部署到 SQL Server 的实例  
  
1.  在目标计算机上打开部署文件夹。  
  
2.  双击清单文件（\<项目名称>.SSISDeploymentManifest），以启动包安装向导。  
  
3.  在 **“部署 SSIS 包”** 页上，选择 **“SQL Server 部署”** 选项。  
  
4.  还可以选择 **“安装后验证包”** ，以便在将包安装到目标服务器之后对其进行验证。  
  
5.  在 **“指定目标 SQL Server”** 页上，指定要将包安装到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，并选择身份验证模式。 如果选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
6.  在 **“选择安装文件夹”** 页上，指定文件系统中用来安装包依赖项的文件夹。  
  
7.  如果包包括配置，可以通过更新“配置包”页上 **“值”** 列表中的值来编辑这些配置。  
  
8.  如果选择了在安装之后验证包，请查看所部署的包的验证结果。  

## <a name="redeployment-of-packages"></a>重新部署包
  在部署项目后，您可能需要更新或扩展包功能，然后重新部署包含更新包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。 在重新部署包的过程中，您应该检查部署实用工具中包括的配置属性。 例如，您可能不希望在重新部署包后允许对配置进行更改。  
  
### <a name="process-for-redeployment"></a>重新部署过程  
 在完成更新包后，您应该重新生成该项目，将部署文件夹复制到目标计算机，然后重新运行包安装向导。  
  
 如果只更新项目中的少数几个包，您可能不希望重新部署整个项目。 若要仅部署几个包，可以新建一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，将更新后的包添加到新的项目，然后生成并部署该项目。 在将包添加到其他项目时，包配置会自动随包一起复制。  

## <a name="package-installation-wizard-ui-reference"></a>包安装向导 UI 参考
  可以使用 **“包安装向导”** 部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目（包括包、所包含的杂项文件以及所有包的依赖关系）。  
  
 在部署包之前，可以先创建配置，然后再将其与包一起进行部署。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在运行时使用配置来动态更新包和包对象的属性。 例如，通过提供将值映射到包含连接字符串的属性的配置，可在运行时动态设置 OLE DB 连接的连接字符串。  
  
 只有在生成 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目并创建部署实用工具后，方可运行包安装向导。 有关详细信息，请参阅 [Deploy Packages by Using the Deployment Utility](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)。  
  
 以下部分介绍了该向导中的各页。  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>“欢迎使用包安装向导”页  
 可以使用 **“包安装向导** ”部署为其生成包部署实用工具的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
 **不再显示此起始页**  
 选择此选项可以在下次运行向导时跳过起始页。  
  
 **Next**  
 转到向导的下一页。  
  
 **“完成”**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="configure-packages-page"></a>“配置包”页  
 可以使用 **“配置包”** 页编辑包配置。  
  
#### <a name="options"></a>“常规”  
 **配置文件**  
 通过从列表中选择文件，可以编辑配置文件的内容。  
  
 **相关主题：**[创建包配置](../../integration-services/packages/create-package-configurations.md)  
  
 **路径**  
 查看要配置的属性的路径。  
  
 **类型**  
 查看属性的数据类型。  
  
 **ReplTest1**  
 指定配置的值。  
  
 **Next**  
 转到向导的下一页。  
  
 **“完成”**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="confirm-installation-page"></a>“确认安装”页  
 可以使用 **“确认安装”** 页开始安装包，查看状态以及查看向导用于从指定项目中安装文件的信息。  
  
 **Next**  
 安装包及其相关文件，并在完成安装后转到下一个向导页。  
  
 **“状态”**  
 显示包的安装进度。  
  
 **“完成”**  
 转到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="deploy-ssis-packages-page"></a>“部署 SSIS 包”页  
 可以使用 **“部署 SSIS 包”** 页指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包及其依赖关系的安装位置。  
  
#### <a name="options"></a>“常规”  
 **部署到文件系统**  
 将包及其依赖关系部署到文件系统内指定的文件夹中。  
  
 **部署到 SQL Server**  
 将包及其依赖关系部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在服务器之间共享包，请使用此选项。 将所有包依赖关系安装在文件系统内指定的文件夹中。  
  
 **安装后验证包**  
 指示安装后是否验证包。  
  
 **Next**  
 转到向导的下一页。  
  
 **“完成”**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="packages-validation-page"></a>“包验证”页  
 可以使用 **“包验证”** 页查看包验证的进度和结果。  
  
 **Next**  
 转到向导的下一页。  
  
### <a name="select-installation-folder-page"></a>“选择安装文件夹”页  
 可以使用 **“选择安装文件夹”** 页，指定在文件系统中安装包及其依赖关系的文件夹。  
  
#### <a name="options"></a>“常规”  
 **文件夹**  
 指定包及其依赖关系要复制到的路径和文件夹。  
  
 **“浏览”**  
 使用“查找文件夹”对话框找到目标文件夹。  
  
 **Next**  
 转到向导的下一页。  
  
 **“完成”**  
 跳到“完成包安装向导”页。 如果已经复查完前面向导页中的选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="specify-target-sql-server-page"></a>“指定目标 SQL Server”页  
 可以使用 **“指定目标 SQL Server”** 页，指定将包部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的选项。  
  
#### <a name="options"></a>“常规”  
 **服务器名称**  
 指定要部署包的服务器的名称。  
  
 **Use Windows Authentication**  
 指定是否使用 Windows 身份验证来登录到服务器。 为了实现更好的安全性，建议使用 Windows 身份验证。  
  
 **使用 SQL Server 身份验证**  
 指定包是否应使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证来登录到服务器。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **User name**  
 指定用户名。  
  
 **密码**  
 指定密码。  
  
 **包路径**  
 指定逻辑文件夹的名称，或者输入 "/" 作为默认文件夹。  
  
 若要在“SSIS 包”对话框中选择该文件夹，请单击“浏览(...)”。但是，该对话框不提供用来选择默认文件夹的方法。 如果要使用默认文件夹，则必须在该文本框中输入 "/"。  
  
> [!NOTE]  
>  如果您没有输入有效的包路径，则会出现下面的错误消息：“一个或多个参数无效”。  
  
 **依靠服务器存储进行加密**  
 选择此项可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的安全功能来帮助保护包。  
  
 **Next**  
 转到向导的下一页。  
  
 **“完成”**  
 跳到“完成包安装向导”页。 如果返回到向导前面的页修改所选项，并指定了所有必需的选项，则可以使用此选项。  
  
### <a name="finish-the-package-installation-page"></a>“完成包安装”页  
 可以使用 **“完成包安装向导”** 页查看包安装结果的摘要。 此页提供了如所部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的名称、已安装的包、配置文件和安装位置等之类的详细信息。  
  
 **“完成”**  
 单击“完成”即可退出该向导。  

