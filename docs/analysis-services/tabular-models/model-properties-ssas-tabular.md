---
title: "模型属性 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.wspacedbconfig.f1
- sql13.asvs.bidtoolset.fileprop.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f0f897572dda34193a87cab649cb3d1b9e155fcb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="model-properties-ssas-tabular"></a>模型属性（SSAS 表格）
  本主题介绍表格模型属性。 SQL Server 开发工具中的每个表格模型项目都具有模型属性，这些属性影响生成你正创作的模型的方式、备份模型的方式以及存储工作区数据库的方式。 此处所描述的模型属性并不适用于已部署的模型。  
  
 本主题的内容：  
  
-   [模型属性](#bkmk_model_properties)  
  
-   [配置模型属性设置](#bkmk_conf_model_prop)  
  
##  <a name="bkmk_model_properties"></a> 模型属性  
 **高级**  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**生成操作**|编译|此属性指定文件如何与生成和部署过程相关。 此属性设置具有以下选项：<br /><br /> **编译** – 将发生常规的生成操作。 针对模型对象的定义将写入 .asdatabase 文件中。<br /><br /> **无** – 到 .asdatabase 文件的输出将为空。|  
|**复制到输出目录**|不复制|此属性指定源文件将复制到输出目录。 此属性设置具有以下选项：<br /><br /> **不复制** – 在输出目录中不创建任何副本。<br /><br /> **始终复制** – 始终在输出目录中创建副本。<br /><br /> **如果较新则复制** - 只有在存在对 model.bim 文件的更改时，才在输出目录中创建副本。|  
  
 **杂项**  
  
> [!NOTE]  
>  某些属性是在创建模型时自动设置的，不能更改。  
  
> [!NOTE]  
>  在创建新模型项目时，“工作区服务器”、“工作区保持期”和“数据备份”属性将应用默认设置。 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改新模型的默认设置。 可以在“属性”窗口中为每个模型设置这些属性以及其他属性。 有关详细信息，请参阅 [配置默认数据建模和部署属性（SSAS 表格）](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**排序规则**|用于安装 Visual Studio 的计算机的默认排序规则。|模型的排序规则指示符。|  
|**兼容级别**|默认值或在创建项目时选择的其他值。|适用于 SQL Server 2012 Analysis Services SP1 或更高版本。 指定可用于此模型的功能和设置。 有关详细信息，请参阅 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|**数据备份**|不备份到磁盘|指定模型数据的备份是否将保留在备份文件中。 此属性设置具有以下选项：<br /><br /> **备份到磁盘** - 指定将模型数据的备份保留在磁盘上。 在保存模型时，数据也将保存到备份 (ABF) 文件中。 选择此选项可能导致保存和加载模型的速度变慢<br /><br /> **不备份到磁盘** - 指定不将模型数据的备份保留在磁盘上。 此选项将保存时间和模型加载时间降至最低。<br /><br /> <br /><br /> 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改此属性的默认设置。| 
|**默认筛选器方向**|单方向|确定新关系的默认筛选器方向。| 
|**DirectQuery 模式**|Off|指定此模型是否在 DirectQuery 模式下操作。 有关详细信息，请参阅 [DirectQuery 模式（SSAS 表格）](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。|  
|**文件名**|Model.bim|指定 .bim 文件的名称。 该文件名不应更改。|  
|**完整路径**|在创建项目时指定的路径。|Model.bim 文件位置。 不能在“属性”窗口中设置此属性。|  
|**语言**|英语|模型的默认语言。 该默认语言由 Visual Studio 语言确定。 不能在“属性”窗口中设置此属性。|  
|**工作区数据库**|项目名称，后跟一个下划线，再后跟一个 GUID。|用于存储和编辑所选 model.bim 文件的内存中模型的工作区数据库的名称。 此数据库将出现在“工作区服务器”属性中指定的 Analysis Services 实例中。 不能在“属性”窗口中设置此属性。 有关详细信息，请参阅[工作区数据库（SSAS 表格）](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)。|  
|**工作区保持期**|从内存中卸载|指定在关闭某一模型后将如何保留工作区数据库。 工作区数据库将包括模型元数据、导入到模型中的数据以及模拟凭据（已加密）。 在某些情况下，工作区数据库可能会非常大并且占用大量内存。 默认情况下，工作区数据库将从内存中卸载。 在更改此设置时，一定要考虑您的可用内存资源以及计划处理该模型的频繁程度。 此属性设置具有以下选项：<br /><br /> **保留在内存中** - 指定在关闭模型后将工作区数据库保留在内存中。 此选项将会占用较多内存；但打开某一模型时，将会占用较少的资源并且工作区数据库将更快加载。<br /><br /> **从内存中卸载** - 指定将工作区数据库保留在磁盘上，但在关闭模型后将不再保留在内存中。 此选项将会占用较少内存；但打开某一模型时，将会占用附加的资源，并且与工作区数据库保留在内存中相比，模型的加载速度将更慢。 在内存中资源受到限制或在处理远程工作区数据库时，将使用此选项。<br /><br /> **删除工作区** - 指定从内存中删除工作区数据库，在关闭模型后不将工作区数据库保留在磁盘上。 此选项将会占用较少内存和存储空间；但打开某一模型时，将会占用附加的资源，并且与工作区数据库保留在内存中或磁盘上相比，模型的加载速度将更慢。 只有在偶尔处理模型时，才使用此选项。<br /><br /> <br /><br /> 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改此属性的默认设置。|  
|**工作区服务器**|localhost|此属性指定创作模型时将用于承载工作区数据库的默认服务器。 在本地计算机上运行的 Analysis Services 的所有可用实例都将包括在列表框中。<br /><br /> 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改此属性的默认设置。<br /><br /> <br /><br /> 注意：建议你始终将一个本地 Analysis Services 服务器指定为工作区服务器。 对于远程服务器上的工作区数据库，不支持从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 进行导入，数据不能在本地备份，并且在查询过程中用户界面可能会遇到滞后的情况。|  
  
##  <a name="bkmk_conf_model_prop"></a> 配置模型属性设置  
  
1.  在 SSDT 的“解决方案资源管理器” 中，单击 **Model.bim** 文件。  
  
2.  在 **“属性”** 窗口中，单击某个属性，然后键入值或单击向下箭头选择设置选项。  
  
## <a name="see-also"></a>另请参阅  
 [配置默认数据建模和部署属性（SSAS 表格）](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [项目属性（SSAS 表格）](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
