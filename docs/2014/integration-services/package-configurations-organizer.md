---
title: 包配置组织程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.packageconfigurationorganizer.f1
helpviewer_keywords:
- Package Configurations Organizer dialog box
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3b880e23bdc191da1f34f2261d7c87a32f03fb42
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964897"
---
# <a name="package-configurations-organizer"></a>“包配置组织程序”
  可以使用 **“包配置组织程序”** 对话框启用包配置，查看当前包的配置列表以及指定加载这些配置的首选顺序。  
  
> [!NOTE]  
>  配置可用于包部署模型。 对于项目部署模型，参数用于代替配置。 项目部署模型使您可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 有关部署模型的详细信息，请参阅 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 如果多个配置更新同一属性，则在配置列表中排列靠后的配置的值将代替在列表中排列靠前的配置的值。 最后加载到属性中的值是在包运行时将要使用的值。 而且，如果包使用直接配置（例如 XML 配置文件）和间接配置（例如环境变量）的组合，那么指向直接配置的位置的间接配置必须在列表中处于靠前位置。  
  
> [!NOTE]  
>  如果包配置按照首选顺序加载，则配置按照从 **“包配置组织程序”** 对话框中显示的列表顶部到列表底部的顺序进行加载。 但是，在运行时，包配置可能不会按照首选顺序加载。 父包配置将在其他类型的配置之后加载的情况尤其如此。  
  
 在运行时，包配置将更新包对象的属性值。 加载包时，配置中的值将替换开发包时所设置的值。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支持不同的配置类型。 例如，您可以使用包含多个配置的 XML 文件或包含单个配置的环境变量。 有关详细信息，请参阅 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
## <a name="options"></a>选项  
 **启用包配置**  
 选择此选项可对包使用配置。  
  
 **配置名称**  
 查看配置的名称。  
  
 **配置类型**  
 查看存储配置的位置类型。  
  
 **配置字符串**  
 查看存储配置值的位置。 该位置可以是文件路径、环境变量的名称、父级包变量的名称、注册表项或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表的名称。  
  
 **目标对象**  
 查看配置更新的对象的名称。 如果配置是 XML 配置文件或 SQL Server 表，则列为空，因为配置可以包含多个对象。  
  
 **Target 属性**  
 查看配置修改的属性的名称。 如果配置类型支持多个配置，则此列为空白。  
  
 **添加**  
 通过使用包配置向导来添加配置。  
  
 **编辑**  
 通过重新运行包配置向导来编辑现有配置。  
  
 **删除**  
 选择一个配置，再单击“删除”。****  
  
 **箭头**  
 在列表中选择一个配置，再使用向上键和向下键可将其上移或下移。 配置将按照在列表中的显示顺序来进行加载。  
  
## <a name="see-also"></a>另请参阅  
 [创建包配置](../../2014/integration-services/create-package-configurations.md)  
  
  
