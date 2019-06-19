---
title: 包配置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package configuration syntax [Integration Services]
- SQL Server Integration Services packages, configurations
- SSIS packages, configurations
- XML [Integration Services]
- Integration Services packages, configurations
- configuration syntax [Integration Services]
- indirect configurations [Integration Services]
- configurations [Integration Services]
- direct configurations [Integration Services]
- packages [Integration Services], configurations
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c220fc87f726d8ba3d8e8cc92904ce42e3baeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056886"
---
# <a name="package-configurations"></a>包配置
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供可用于在运行时更新属性值的包配置。  
  
> [!NOTE]  
>  配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [部署的项目和包](packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 配置是添加到已完成包中的属性/值对。 通常，在包开发期间您在包对象上创建包设置属性，然后将配置添加到包中。 当包运行时，它从配置中获取新的属性值。 例如，通过使用配置，您可以更改连接管理器的连接字符串，或者更新变量的值。  
  
 包配置具有下列优点：  
  
-   使用配置可以更轻松地将包从开发环境转移到生产环境中。 例如，配置可以更新源文件的路径，或者更改数据库或服务器的名称。  
  
-   将包部署到多台不同的服务器时，配置非常有用。 例如，用于每个已部署包的配置中的变量可以包含不同的磁盘空间，并且如果可用磁盘空间不满足此值，包将不会运行。  
  
-   配置可以使包更加灵活。 例如，配置可以更新在属性表达式中使用的变量的值。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支持几种不同的存储包配置（例如 XML 文件、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的表以及环境变量和包变量）的方法。  
  
 每个配置都是一个属性/值对。 XML 配置文件和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置类型可以包括多个配置。  
  
 在创建用于安装包的包部署实用工具时将会包括这些配置。 在安装包时，可以在安装包的过程中更新配置。  
  
## <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>了解在运行时如何应用包配置  
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
  
 有关这些选项以及这些选项的行为之间的区别的详细信息[!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]和早期版本中，请参阅[SQL Server 2014 中 Integration Services 功能的行为更改](../../2014/integration-services/behavior-changes-to-integration-services-features-in-sql-server-2014.md)。  
  
## <a name="package-configuration-types"></a>包配置类型  
 下表介绍了包配置的类型。  
  
|类型|描述|  
|----------|-----------------|  
|XML 配置文件|XML 文件包含配置。 XML 文件可以包括多个配置。|  
|环境变量|环境变量包含配置。|  
|注册表项|注册表项包含配置。|  
|父包变量|包中的变量包含配置。 此配置类型通常用于更新子包中的属性。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的表包含配置。 表可以包括多个配置。|  
  
### <a name="xml-configuration-files"></a>XML 配置文件  
 如果选择 **“XML 配置文件”** 配置类型，您可以创建一个新的配置文件；重用现有文件并添加新的配置；也可以重用现有文件但覆盖现有文件的内容。  
  
 XML 配置文件包括两部分：  
  
-   包含有关配置文件信息的标题。 此元素包括的属性有该文件的创建时间和该文件的创建者的姓名等。  
  
-   包含有关每个配置的信息的配置元素。 此元素包括的特性有属性路径和属性的配置值等。  
  
 下列 XML 代码说明了 XML 配置文件的语法。 此示例显示了一个名为 `MyVar`的整数变量的 Value 属性配置。  
  
```  
<?xml version="1.0"?>  
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
  
### <a name="registry-entry"></a>注册表项  
 如果要使用注册表项存储配置，可以使用已有项或在 HKEY_CURRENT_USER 中创建新项。 使用的注册表项必须具有名为 `Value` 的值。 该值可以是 DWORD 或一个字符串。  
  
 如果选择 **“注册表项”** 配置类型，请在“注册表项”框中键入注册表项的名称。 格式为 \<registry key>。 如果要使用不在 HKEY_CURRENT_USER 根目录下的注册表项，请使用 \<Registry key\registry key\\...> 格式来标识该项。 例如，若要使用 SSISPackages 中的 MyPackage 项，请键入 `SSISPackages\MyPackage`。  
  
### <a name="sql-server"></a>SQL Server  
 如果选择 **SQL Server** 配置类型，则需指定到要存储这些配置的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的连接。 可以将配置保存到现有表，也可以在指定数据库中新建表。  
  
 下面的 SQL 语句说明了包配置向导提供的默认 CREATE TABLE 语句。  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 您为配置提供的名称就是在 **ConfigurationFilter** 列中存储的值。  
  
## <a name="direct-and-indirect-configurations"></a>直接配置和间接配置  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了直接配置和间接配置。 如果直接指定配置， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 会在配置项和包对象属性之间创建直接链接。 如果源的位置不更改，则直接配置是较好的选择。 例如，如果确定包中的所有部署都使用相同的文件路径，则可以指定一个 XML 配置文件。  
  
 间接配置使用环境变量。 配置不直接指定配置设置，而是指向环境变量，环境变量又包含配置值。 如果对于包的每个部署，配置的位置都可以更改，则使用间接配置是较好的选择。  
  
## <a name="related-tasks"></a>Related Tasks  
 [创建包配置](../../2014/integration-services/create-package-configurations.md)  
  
## <a name="related-content"></a>相关内容  
  
-   msdn.microsoft.com 上的技术文章 [理解 Integration Services 包配置](https://go.microsoft.com/fwlink/?LinkId=165643)  
  
-   博客文章[代码的包配置中创建包](https://go.microsoft.com/fwlink/?LinkId=217663)，www.sqlis.com 上的。  
  
-   博客文章[API 示例-以编程方式将配置文件添加到包](https://go.microsoft.com/fwlink/?LinkId=217664)，blogs.msdn.com 上的。  
  
  
