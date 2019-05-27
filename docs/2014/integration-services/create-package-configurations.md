---
title: 创建包配置 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 287ac1a5631cf2e3925e5895db7f04bb7b89bf5d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060169"
---
# <a name="create-package-configurations"></a>创建包配置
  使用 **“包配置组织程序”** 对话框和包配置向导，可以创建包配置。 若要访问这些工具，请在 **中单击** “SSIS” **菜单上的** “包配置” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
> [!NOTE]  
>  您还可以通过单击 **“配置”** 属性旁的省略号按钮，访问 **“包配置组织程序”** 。 “配置”选项出现在包的属性窗口中。  
  
> [!NOTE]  
>  配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [部署的项目和包](packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 在 **“包配置组织程序”** 对话框中，可以启用包以使用配置、添加和删除配置以及设置加载配置的首选顺序。  
  
> [!NOTE]  
>  如果包配置按照首选顺序加载，则配置按照从 **“包配置组织程序”** 对话框中显示的列表顶部到列表底部的顺序进行加载。 但是，在运行时，包配置可能不会按照首选顺序加载。 尤其是，父包配置将在其他类型的配置之后加载。  
  
> [!NOTE]  
>  如果多个配置设置相同的对象属性，则在运行时使用最后加载的值。  
  
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
  
> [!NOTE]  
>  包配置向导的最后一页“完成向导”列出了配置中的目标属性。 如果希望通过使用 **dtexec** 命令提示符实用工具在运行包时更新属性，则可以通过运行包配置向导来生成表示属性路径的字符串，然后将它们复制并粘贴到命令提示符窗口中，以便用于 **dtexec** 的设置选项。  
  
 下表介绍 **“包配置组织程序”** 对话框的配置列表中的各列。  
  
|“列”|Description|  
|------------|-----------------|  
|**配置名称**|配置的名称。|  
|**配置类型**|配置类型。|  
|**配置字符串**|配置的位置。 位置可以是路径、环境变量、注册表项、父包变量名或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的表。|  
|**目标对象**|其属性具有配置的对象的名称。 如果配置是 XML 配置文件，则该列为空，因为该配置可以更新多个对象。|  
|**目标属性**|属性的名称。 如果配置写入 XML 配置文件或 SQL Server 表，则列为空，因为配置可以更新多个对象。|  
  
### <a name="to-create-a-package-configuration"></a>创建包配置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“控制流”**、 **“数据流”**、 **“事件处理程序”** 或 **“包资源管理器”** 选项卡。  
  
4.  在 **SSIS** 菜单上，单击“包配置” 。  
  
5.  在 **“包配置组织程序”** 对话框中，选择 **“启用包配置”**，再单击 **“添加”**。  
  
6.  在“包配置向导”页的欢迎页上，单击 **“下一步”**。  
  
7.  在“选择配置类型”页上，指定配置类型，然后设置与该配置类型相关的属性。 有关详细信息，请参阅 [包配置向导用户界面参考](../../2014/integration-services/package-configuration-wizard-ui-reference.md)。  
  
8.  在“选择要导出的属性”页上，选择要在配置中包括的包对象的属性。 如果配置类型只支持一个属性，则此向导页的标题是“选择目标属性”。 有关详细信息，请参阅 [包配置向导用户界面参考](../../2014/integration-services/package-configuration-wizard-ui-reference.md)。  
  
    > [!NOTE]  
    >  只有 **XML 配置文件**和 **SQL Server** 配置类型支持在一个配置中包括多个属性。  
  
9. 在“完成向导”页上，键入配置的名称，然后单击 **“完成”**。  
  
10. 查看 **“包配置组织程序”** 对话框中的配置。  
  
11. 单击 **“关闭”**。  
  
## <a name="external-resources"></a>外部资源  
  
-   msdn.microsoft.com 上的技术文章 [理解 Integration Services 包配置](https://go.microsoft.com/fwlink/?LinkId=165643)   
  
-   博客文章[代码的包配置中创建包](https://go.microsoft.com/fwlink/?LinkId=217663)，www.sqlis.com 上的。  
  
-   博客文章[API 示例-以编程方式将配置文件添加到包](https://go.microsoft.com/fwlink/?LinkId=217664)，blogs.msdn.com 上的。  
  
## <a name="see-also"></a>请参阅  
 [“包配置”](../../2014/integration-services/package-configurations.md)   
 [打包部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [以编程方式使用变量](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  
