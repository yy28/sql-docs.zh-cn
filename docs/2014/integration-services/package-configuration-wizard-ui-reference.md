---
title: 包配置向导 UI 参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.configwizard.selectobjects.f1
- sql12.dts.configwizard.selecconfigtype.f1
- sql12.dts.configwizard.finishdtsconfiguration.f1
- sql12.dts.configwizard.welcome.f1
ms.assetid: adca6938-6d5a-40ec-950e-dceb79d044fe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 042f1146295d0a8358a7f89a38929a77e6f761a1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376185"
---
# <a name="package-configuration-wizard-ui-reference"></a>包配置向导用户界面参考
  可以使用 **“包配置向导”** 创建在运行时更新 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包及其对象的属性的配置。 当您在 **“包配置组织程序”** 对话框中添加新配置或者修改现有配置时，将运行该向导。 若要打开 **“包配置组织程序”** 对话框，请在 **上的** SSIS **菜单中选择** “包配置” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 有关详细信息，请参阅 [创建包配置](../../2014/integration-services/create-package-configurations.md)。  
  
> [!NOTE]  
>  配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 以下部分介绍了该向导中的各页。  
  
## <a name="welcome-to-the-package-configuration-wizard-page"></a>“欢迎使用包配置向导”页  
 使用 **“SSIS 配置向导”** 可以创建在运行时更新包及其对象的属性的配置。  
  
### <a name="options"></a>选项  
 **不再显示此页**  
 下次打开向导时跳过欢迎页。  
  
 **Next**  
 转到向导的下一页。  
  
## <a name="select-configuration-type-page"></a>“选择配置类型”页  
 使用 **“选择配置类型”** 页可以指定要创建的配置类型。  
  
 如果需要其他信息才能确定要使用的配置类型，则请参阅 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
### <a name="static-options"></a>静态选项  
 **配置类型**  
 使用下列选项选择存储配置的源的类型：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**XML 配置文件**|将配置存储为 XML 文件。 选择此值将显示 **“配置类型”** 部分中的动态选项。|  
|**环境变量**|将配置存储在一个环境变量中。 选择此值将显示 **“配置类型”** 部分中的动态选项。|  
|**注册表项**|将配置存储在注册表中。 选择此值将显示 **“配置类型”** 部分中的动态选项。|  
|**父包变量**|将配置存储为包含该任务的包中的变量。  选择此值将显示 **“配置类型”** 部分中的动态选项。|  
|**SQL Server**|将配置存储在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]表中。 选择此值将显示 **“配置类型”** 部分中的动态选项。|  
  
 **Next**  
 查看向导的下一页。  
  
### <a name="dynamic-options"></a>动态选项  
  
#### <a name="configuration-type-option--xml-configuration-file"></a>配置类型选项 = XML 配置文件  
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
  
#### <a name="configuration-type-option--environment-variable"></a>配置类型选项 = 环境变量  
 **环境变量**  
 选择包含配置信息的环境变量。  
  
#### <a name="configuration-type-option--registry-entry"></a>配置类型选项 = 注册表项  
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
  
#### <a name="configuration-type-option--parent-package-variable"></a>配置类型选项 = 父包变量  
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
  
#### <a name="configuration-type-options--sql-server"></a>配置类型选项 = SQL Server  
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
  
## <a name="select-objects-to-export-page"></a>“选择要导出的对象”页  
 使用 **“选择目标属性”** 或“选择要导出的属性”页可以指定配置包含的对象属性。 只有在选择 XML 配置类型时，才能选择多个属性。  
  
### <a name="options"></a>选项  
 **对象**  
 展开包层次结构并选择要导出的属性。  
  
 **属性特性**  
 查看属性的特性。  
  
 **Next**  
 转到向导的下一页。  
  
## <a name="completing-the-wizard-page"></a>“完成向导”页  
 使用 **“完成向导”** 页可以提供配置的名称以及查看此向导用于创建配置的设置。 在向导完成之后，将显示 **“包配置组织程序”** ，其中列出了包的所有配置。  
  
### <a name="options"></a>选项  
 **配置名称**  
 键入配置的名称。  
  
 **预览**  
 查看此向导用于创建配置的设置。  
  
 **“完成”**  
 创建配置并退出 **包配置向导**。  
  
## <a name="see-also"></a>请参阅  
 [创建包配置](../../2014/integration-services/create-package-configurations.md)  
  
  
