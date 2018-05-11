---
title: 从 Analysis Services 导入 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b527e648912e7a7a6e11a1aea5d0c1d05d31486e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="import-from-analysis-services"></a>从 Analysis Services 导入 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍如何通过使用从服务器中的项目模板中导入从现有的表格模型中导入元数据创建新的表格模型项目[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>通过从 Analysis Services 的现有模型中导入元数据来创建新的模型  
 您可以使用“从服务器导入”项目模板从 Analysis Services 服务器上的现有表格模型复制元数据，来创建新的表格模型项目。 创建的新项目将具有与从中导入该项目的模型相同的数据源连接、表、关系、度量值、KPI、角色、层次结构、透视和分区。 但是，数据不会从现有模型复制到新的模型工作区。 完成导入过程且创建新模型项目后，您必须运行“全部处理”将数据从数据源加载到新的模型项目工作区数据库中。  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>通过从现有模型中导入元数据来创建新的模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在 **“新建项目”** 对话框中，在 **“已安装的模板”**下，单击 **“商业智能”**，然后单击 **“从服务器导入”**。  
  
3.  在 **“名称”**中，键入项目的名称，然后指定位置和解决方案名称，再单击 **“确定”**。  
  
4.  在 **“从 Analysis Services 导入”** 对话框的 **“服务器名称”**中，指定包含您要导入的模型元数据的 Analysis Services 服务器的名称。  
  
5.  在 **“数据库名称”**中，选择包含您要导入的模型元数据的表格模型数据库，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [项目属性](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
