---
title: 确定服务器模式的 Analysis Services 实例 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b292e20880dcb77c4f448f7e141355edff67417f
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578997"
---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>确定 Analysis Services 实例的服务器模式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 可以安装在以下三种服务器模式之一下：多维和数据挖掘 （默认值）， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 和表格。 Analysis Services 实例的服务器模式在安装过程中在您选择用于安装服务器的选项时确定。  
  
 服务器模式确定您创建和部署的解决方案的类型。 如果您没有安装服务器软件并且想要知道服务器安装在哪一模式下，则可以使用本主题中的信息确定该模式。 有关特定模式中功能可用性的详细信息，请参阅[比较表格和多维解决方案](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)。  
  
 如果您不想使用所安装的服务器模式，则必须卸载后再重新安装该软件，并且选择想要的模式。 或者，您可以在同一台计算机上安装 Analysis Services 的其他实例，以便您具有运行不同模式的多个实例。  
  
## <a name="server-icons-in-object-explorer"></a>对象资源管理器中的服务器图标  
 确定服务器模式的最简单方法是在 SQL Server Management Studio 中连接到该服务器，并且在对象资源管理器中注意服务器名称旁的图标。 下图显示在多维、表格和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模式下部署的三个 Analysis Services 实例：  
  
 ![对象资源管理器图标，为每个服务器模式](../../analysis-services/instances/media/ssas-ssms-servermodes.gif "每种服务器模式的对象资源管理器图标")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>在 MSMDSRV.INI 文件中查看 DeploymentMode 属性  
 或者，您可以在包含在每个 Analysis Services 实例中的 msmdsrv.ini 文件中查看 **DeploymentMode** 属性。 该属性的值标识服务器模式。 有效值为 0（多维）、1 (SharePoint) 或 2（表格）。 你必须是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员（即，服务器角色的成员）才可以打开 msmdsrv.ini 文件。 此文件包含结构化的 XML。 可以使用记事本或其他文本编辑器查看该文件。  
  
> [!CAUTION]  
>  不要更改 **DeploymentMode** 属性的值。 不支持在安装服务器后手动更改该属性。  
  
## <a name="about-the-deploymentmode-property"></a>关于 DeploymentMode 属性  
 **DeploymentMode** 属性确定 Analysis Services 服务器实例的操作上下文。 此属性称为服务器模式对话框、 消息和文档中。 此属性基于您安装 Analysis Services 的方式由安装程序启动。 只应考虑在内部使用此属性，并且始终使用安装程序指定的值。  
  
 此属性的有效值包括以下项：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|这是默认值。 它指定多维模式，用于支持使用 MOLAP、HOLAP 和 ROLAP 存储以及数据挖掘模型的多维数据库。|  
|1|指定 Analysis Services 实例已作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署的一部分安装。 不要更改作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装的一部分的 Analysis Services 实例的部署模式属性。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据将不再在该服务器上运行。|  
|2|指定用于承载使用内存中存储或 DirectQuery 存储的表格模型数据库的表格模式。|  
  
 每个模式与其他模式都是互斥的。 配置为表格模式的服务器不能运行包含多维数据集和维度的 Analysis Services 数据库。 如果基础计算机硬件能够支持，则您可以在同一台计算机上安装 Analysis Services 的多个实例并且对每个实例进行配置以便使用不同的部署模式。 请记住，Analysis Services 是一种消耗大量资源的应用程序。 仅推荐对于高端服务器，才在同一个系统上部署多个实例。  
  
## <a name="see-also"></a>请参阅  
 [安装 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [在多维和数据挖掘模式下安装 Analysis Services](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [表格模型解决方案](../../analysis-services/tabular-models/tabular-models-ssas.md)   
 [多维模型解决方案](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
