---
title: "从 Analysis Services (SSAS 表格) 导入 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81cee939240fd9379f2c521443272ae478de6243
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="import-from-analysis-services-ssas-tabular"></a>从 Analysis Services 导入（SSAS 表格）
  本主题介绍如何通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“从服务器导入”项目模板从现有的表格模型导入元数据，创建新的表格模型项目。  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>通过从 Analysis Services 的现有模型中导入元数据来创建新的模型  
 您可以使用“从服务器导入”项目模板从 Analysis Services 服务器上的现有表格模型复制元数据，来创建新的表格模型项目。 创建的新项目将具有与从中导入该项目的模型相同的数据源连接、表、关系、度量值、KPI、角色、层次结构、透视和分区。 但是，数据不会从现有模型复制到新的模型工作区。 完成导入过程且创建新模型项目后，您必须运行“全部处理”将数据从数据源加载到新的模型项目工作区数据库中。  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>通过从现有模型中导入元数据来创建新的模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在 **“新建项目”** 对话框中，在 **“已安装的模板”**下，单击 **“商业智能”**，然后单击 **“从服务器导入”**。  
  
3.  在 **“名称”**中，键入项目的名称，然后指定位置和解决方案名称，再单击 **“确定”**。  
  
4.  在 **“从 Analysis Services 导入”** 对话框的 **“服务器名称”**中，指定包含您要导入的模型元数据的 Analysis Services 服务器的名称。  
  
5.  在 **“数据库名称”**中，选择包含您要导入的模型元数据的表格模型数据库，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [项目属性（SSAS 表格）](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  

