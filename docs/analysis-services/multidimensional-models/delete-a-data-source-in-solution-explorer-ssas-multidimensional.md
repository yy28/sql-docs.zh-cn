---
title: 删除数据源在解决方案资源管理器 (SSAS 多维) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 95ab77b284756baa712e858027b71e7d64eba4c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>在解决方案资源管理器中删除数据源（SSAS 多维）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以删除某一数据源对象以便从 Analysis Services 多维模型项目中永久删除该对象。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，数据源提供了构造数据源视图的基础，而后，数据源视图用于定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或数据库中的维度、多维数据集和挖掘结构。 因此，删除数据源可能会导致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象无效。 您应该始终在删除对象前查看提供的依赖对象的列表。  
  
> [!IMPORTANT]  
>  无法从处于联机模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 打开的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库中删除其他对象所依赖的数据源。 要删除该数据源，必须先删除 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中所有依赖该数据源的对象。 有关联机模式的详细信息，请参阅 [在联机模式下连接到 Analysis Services 数据库](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。  
  
### <a name="to-delete-a-data-source"></a>删除数据源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要从其中删除数据源的项目或连接到要从其中删除数据源的数据库。  
  
2.  在 **“解决方案资源管理器”**中，展开 **“数据源”** 文件夹。  
  
3.  右键单击数据源，然后单击“删除”。 **“删除对象”**  对话框将出现，其中显示您删除数据源后将失效的对象。 在单击 **“确定”** 以便删除数据源之前请仔细查看此列表。  
  
4.  保存项目。  
  
     在从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中删除数据源后，必须保存已修改的项目，否则下次打开此项目时将会收到错误，因为当项目尝试加载已删除的数据源时，此数据源的基础 XML 文件将会丢失。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支持的数据源（SSAS - 多维）](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
