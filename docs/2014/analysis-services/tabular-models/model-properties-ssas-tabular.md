---
title: 模型属性（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.fileprop.f1
- sql12.asvs.bidtoolset.wspacedbconfig.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
author: minewiskan
ms.author: owend
ms.openlocfilehash: d4106377f2aadfec9173076ece3cf8bf4bc7d183
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938798"
---
# <a name="model-properties-ssas-tabular"></a>模型属性（SSAS 表格）
  本主题介绍表格模型属性。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的每个表格模型项目都具有模型属性，这些属性影响生成您正创作的模型的方式、备份模型的方式以及存储工作区数据库的方式。 此处所描述的模型属性并不适用于已部署的模型。  
  
 本主题的内容：  
  
-   [模型属性](#bkmk_model_properties)  
  
-   [配置模型属性设置](#bkmk_conf)  
  
##  <a name="model-properties"></a><a name="bkmk_model_properties"></a>模型属性  
 **高级**  
  
|属性|默认设置|说明|  
|--------------|---------------------|-----------------|  
|**生成操作**|Compile|此属性指定文件如何与生成和部署过程相关。 此属性设置具有以下选项：<br /><br /> **编译**-正常生成操作发生。 针对模型对象的定义将写入 .asdatabase 文件中。<br /><br /> **无**-.Asdatabase 文件的输出将为空。|  
|**复制到输出目录**|不复制|此属性指定源文件将复制到输出目录。 此属性设置具有以下选项：<br /><br /> 不**复制**-在输出目录中不创建任何副本。<br /><br /> **始终复制**-始终在输出目录中创建副本。<br /><br /> **如果较新则复制** - 只有在存在对 model.bim 文件的更改时，才在输出目录中创建副本。|  
  
 **其他**  
  
> [!NOTE]  
>  某些属性是在创建模型时自动设置的，不能更改。  
  
> [!NOTE]  
>  在创建新模型项目时，“工作区服务器”、“工作区保持期”和“数据备份”属性将应用默认设置。 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改新模型的默认设置。 可以在“属性”窗口中为每个模型设置这些属性以及其他属性。 有关详细信息，请参阅 [配置默认数据建模和部署属性（SSAS 表格）](properties-ssas-tabular.md)。  
  
|属性|默认设置|说明|  
|--------------|---------------------|-----------------|  
|**排序规则**|用于安装 Visual Studio 的计算机的默认排序规则。|模型的排序规则指示符。|  
|**兼容性级别**|默认值或在创建项目时选择的其他值。|适用于 SQL Server 2012 Analysis Services SP1 或更高版本。 指定可用于此模型的功能和设置。 有关详细信息，请参阅[&#40;SSAS 表格 SP1&#41;兼容级别](compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|**数据备份**|不备份到磁盘|指定模型数据的备份是否将保留在备份文件中。 请注意，可以在 "位于对话框" 对话框中 Analysis Server "设置" 中的 "数据建模" 页上更改此属性的默认设置。 此属性设置具有以下选项：<br /><br /> **备份到磁盘** - 指定将模型数据的备份保留在磁盘上。 在保存模型时，数据也将保存到备份 (ABF) 文件中。 选择此选项可能导致保存和加载模型的速度变慢<br /><br /> **不备份到磁盘** - 指定不将模型数据的备份保留在磁盘上。 此选项将保存时间和模型加载时间降至最低。|  
|**DirectQuery 模式**|关|指定此模型是否在 DirectQuery 模式下操作。 有关详细信息，请参阅 [DirectQuery 模式（SSAS 表格）](directquery-mode-ssas-tabular.md)。|  
|**文件名**|Model.bim|指定 .bim 文件的名称。 该文件名不应更改。|  
|**完整路径**|在创建项目时指定的路径。|Model.bim 文件位置。 不能在“属性”窗口中设置此属性。|  
|**语言**|英语|模型的默认语言。 该默认语言由 Visual Studio 语言确定。 不能在“属性”窗口中设置此属性。|  
|**工作区数据库**|项目名称，后跟一个下划线，再后跟一个 GUID。|用于存储和编辑所选 model.bim 文件的内存中模型的工作区数据库的名称。 此数据库将出现在“工作区服务器”属性中指定的 Analysis Services 实例中。 不能在“属性”窗口中设置此属性。 有关详细信息，请参阅[工作区数据库（SSAS 表格）](workspace-database-ssas-tabular.md)。|  
|**工作区保持期**|从内存中卸载|指定在关闭某一模型后将如何保留工作区数据库。 工作区数据库将包括模型元数据、导入到模型中的数据以及模拟凭据（已加密）。 在某些情况下，工作区数据库可能会非常大并且占用大量内存。 默认情况下，工作区数据库将从内存中卸载。 在更改此设置时，一定要考虑您的可用内存资源以及计划处理该模型的频繁程度。 请注意，可以在 "位于对话框" 对话框中 Analysis Server "设置" 中的 "数据建模" 页上更改此属性的默认设置。 此属性设置具有以下选项：<br /><br /> **保留在内存中** - 指定在关闭模型后将工作区数据库保留在内存中。 此选项将会占用较多内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用较少的资源并且工作区数据库将更快加载。<br /><br /> **从内存中卸载** - 指定将工作区数据库保留在磁盘上，但在关闭模型后将不再保留在内存中。 此选项将会占用较少内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区保留在内存中相比，模型的加载速度将更慢。 在内存中资源受到限制或在处理远程工作区数据库时，将使用此选项。<br /><br /> **删除工作区** - 指定从内存中删除工作区数据库，在关闭模型后不将工作区数据库保留在磁盘上。 此选项将会占用较少内存和存储空间；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区数据库保留在内存中或磁盘上相比，模型的加载速度将更慢。 只有在偶尔处理模型时，才使用此选项。|  
|**工作区服务器**|localhost|此属性指定在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创作模型时将用于承载工作区数据库的默认服务器。 在本地计算机上运行的 Analysis Services 的所有可用实例都将包括在列表框中。<br /><br /> 注意：建议你始终将本地 Analysis Services 服务器指定为工作区服务器。 对于远程服务器上的工作区数据库，不支持从 PowerPivot 进行导入，数据不能在本地备份，并且在查询过程中用户界面可能会遇到滞后的情况。<br /><br /> 可以在“数据建模”页（位于“工具\选项”对话框的“Analysis Server”设置中）更改此属性的默认设置。|  
  
##  <a name="bkmk_conf_model_prop"></a>   
###  <a name="to-configure-model-property-settings"></a><a name="bkmk_conf"></a>配置模型属性设置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 **解决方案资源管理器**中，单击 **Model.bim** 文件。  
  
2.  在 **“属性”** 窗口中，单击某个属性，然后键入值或单击向下箭头选择设置选项。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;配置默认数据建模和部署属性](properties-ssas-tabular.md)   
 [项目属性（SSAS 表格）](project-properties-ssas-tabular.md)  
  
  
