---
title: 配置 Analysis Services 项目属性 (SSDT) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 582780b5c0e0a81fed17f4d4113c649063b00f46
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>配置 Analysis Services 项目属性 (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目是使用特定默认属性定义的，这些属性影响 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的生成和部署。  
  
 若要更改项目属性，请右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象，再单击“属性”。 或者，您可以单击“项目”菜单上的 **“属性”** 。  
  
## <a name="property-description"></a>属性说明  
 下表说明每个项目的属性，列出其默认值，并提供有关更改属性值的信息。  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|生成/部署服务器版本|用于部署项目的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|指定最终要将项目部署到其中的服务器的版本。 当多个开发人员共同处理项目时，这些开发人员需要了解服务器版本，以便知道要将哪些功能合并到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。|  
|生成/部署服务器版本|用于开发项目的版本|指定最终要将项目部署到其中的服务器的版本。|  
|生成/输出|/bin|项目生成过程输出的相对路径|  
|生成/删除密码|True|指定是否从在生成过程中写入到输出目录的连接字符串中删除已知密码。 删除密码可提高安全性。 如果删除密码，则在处理已部署项目时需要提供密码，以便 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以访问源数据。|  
|调试/启动对象|\<当前处于活动状态的对象 >|确定启动调试时将要启动的对象。|  
|部署/部署模式|仅部署更改|默认情况下，仅部署对项目对象所做的更改（条件是/前提是没有直接在项目外部对对象进行其他更改）。 您还可以选择在每个部署过程中部署所有项目对象。 为了获得最佳性能，请使用“仅部署更改”。|  
|部署/处理选项|默认|默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在部署对对象所做的更改时确定所需的处理类型。 这通常会使部署时间最短。 但是，您还可以选择在每个部署过程执行完全处理或不执行处理。|  
|部署/事务性部署|False|默认情况下，在处理这些已部署的对象时，已更改对象或所有对象的部署并不是事务性部署。 即使在处理失败时，部署也会成功并且一直保留。 您可以将此默认设置更改为在单个事务中合并部署和处理。|  
|部署/目标服务器|localhost|默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的数据库对象将部署到使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本地计算机上的默认 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 实例。 更改此默认设置以指定本地计算机上的命名实例，或指定您有权创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的任何远程计算机上的任何实例。|  
|部署/数据库|\<项目名称 >|默认情况下，部署时实例化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象所在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的名称是定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时该项目的名称。 更改此属性以更改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上由“服务器”属性指定的数据库的名称。|  
  
## <a name="property-configurations"></a>属性配置  
 基于配置定义属性。 使用项目配置，开发人员可以利用不同的生成、调试和部署设置来处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，而无需直接编辑基础 XML 项目文件。  
  
 项目最初使用单个配置进行创建，此过程称为“开发”。 您可以创建其他配置，并使用配置管理器在配置之间进行切换。  
  
 在创建其他配置之前，所有开发人员均使用此常用配置。 但是，在不同的项目开发阶段（例如在项目的初始开发和测试过程中），不同的开发人员可能会使用不同的数据源并将项目部署到不同的服务器以实现不同目的。 使用配置，您可以将这些不同的设置保留在不同的配置文件中。  
  
## <a name="see-also"></a>另请参阅  
 [生成 Analysis Services 项目 & #40;SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [部署 Analysis Services 项目 & #40;SSDT & #41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
