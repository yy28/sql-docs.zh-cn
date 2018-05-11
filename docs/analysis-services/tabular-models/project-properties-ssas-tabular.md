---
title: 项目属性 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 874f1b6cf24633070935a70425f1dc873aebc7dc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="project-properties"></a>项目属性 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍模型项目属性。 每个表格模型项目都具有一些指定如何部署项目和模型的部署选项和部署服务器属性。 例如，模型将要部署到的服务器和已部署的模型数据库名称。 这些设置与影响模型工作区数据库的模型属性不同。 此处所述的项目属性位于模式属性对话框中，不同于用于显示其他属性类型的属性窗口。 若要显示模式项目属性，请在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]“解决方案资源管理器”中右键单击该项目，然后单击“属性”。  
  
 本主题的内容：  
  
-   [项目属性](#bkmk_proj_properties)  
  
-   [配置“部署选项”和“部署服务器”属性设置](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> 项目属性  
 **部署选项**  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**“处理选项”**|**默认**|默认情况下，Analysis Services 将在部署对对象所做的更改时确定所需的处理类型。 这通常会使部署时间最短。 但是，您还可以选择在每个部署过程执行完全处理或不执行处理。|  
|**事务性部署**|**False**|指定模型的部署是否为事务性的。 默认情况下，在处理这些已部署的对象时，所有对象或已更改对象的部署并不是事务性部署。 即使在处理失败时，部署也会成功并且一直保留。 您可以将此默认设置更改为在单个事务中合并部署和处理。|  
|**查询模式**|**内存中**|指定从中返回查询结果的源。 有关详细信息，请参阅[DirectQuery 模式下](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。|  
  
 **部署服务器**  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|指定一个 Analysis Services 实例。 默认情况下，将模型部署到本地计算机上 Analysis Services 的默认实例。 您可以更改此设置以便指定本地计算机上的命名实例，或指定您有权创建 Analysis Services 对象的任何远程计算机上的任何实例。 通常需要管理员权限。<br /><br /> 可以通过使用“默认部署服务器”属性（位于“工具\选项”对话框的“分析服务器”设置中的“部署”页）更改此属性的默认设置。 有关详细信息，请参阅[配置默认数据建模和部署属性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。|  
|**版本**|**开发人员**|指定模型将部署到的 Analysis Services 服务器的版本。 该服务器版本定义可纳入项目中的不同功能。|  
|**数据库**|**Model**|指定在部署时将实例化的模型对象所处的 Analysis Services 数据库的名称。 该名称将在数据连接或 .rsds 数据连接文件中指定。 建议该名称应反映将使用该模型执行的分析类型，例如 AdventureWorksSalesModel。<br /><br /> 若要防止已部署的模型名称重复，应更改 **“数据库”** 属性名称设置以反映模型的用途。 当用户连接到作为数据源的模型时，他们将看到此名称。|  
|**多维数据集名称**|**Model**|指定报告客户端数据连接中显示的数据库多维数据集名称。|  
|**版本**|**13.0**|项目将部署到的 Analysis Services 实例的版本。|  
  
 **DirectQuery 选项**  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**模拟设置**|**默认**|为在 DirectQuery 模式下运行的模型指定用于连接到数据源的凭据。 这些凭据不同于在默认的内存中模式下使用的模拟凭据。 有关详细信息，请参阅[模拟](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)。|  
  
##  <a name="bkmk_conf_proj_settings"></a> 配置“部署选项”和“部署服务器”属性设置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]“解决方案资源管理器”中右键单击项目，再单击“属性”。  
  
2.  在 **“属性”** 窗口中，单击某个属性，然后键入值或单击向下箭头选择设置选项。  
  
## <a name="see-also"></a>另请参阅  
 [配置默认数据建模和部署属性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [模型属性](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [表格模型解决方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
