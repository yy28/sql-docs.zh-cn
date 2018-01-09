---
title: "授予读取定义权限对象元数据 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 24e661c0ba9bd5c143365c69282e2cdae91b174a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>授予对象元数据的读取定义权限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]权限读取的对象定义或元数据，所选对象上允许管理员授予权限以查看对象的信息，而不用同时授予修改对象的定义、 修改对象的结构，或查看实际的权限该对象的数据。  “读取定义”权限可在数据库、数据源、维度、挖掘结构和挖掘模型级别授予。 如果需要多维数据集的“读取定义”  权限，则必须对数据库启用“读取定义”  。请记住权限是可以累加的。 例如，一个角色授予读取多维数据集的元数据的权限，同时，另一个角色向同一个用户授予读取维度元数据的权限。 两个不同角色的权限合并授予用户在该数据库内的读取多维数据集元数据和维度元数据的权限。  
  
> [!NOTE]  
>  读取数据库元数据的权限是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 连接到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]数据库时所需的最低权限。 可读取元数据的用户还可以使用 DISCOVER_XML_METADATA 架构行集来查询对象并查看其元数据。 有关详细信息，请参阅 [DISCOVER_XML_METADATA 行集](../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)。  
  
## <a name="set-read-definition-permissions-on-a-database"></a>设置数据库的读取定义权限  
 授予读取数据库元数据的权限便同时授予了读取数据库中所有对象的元数据的权限。  
  
 我们建议在为专用处理设置角色时，包括数据库级别的“读取定义”  权限。 拥有“读取定义”权限使得非管理员可以查看 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的模型对象层次结构并导航至单个对象进行后续处理。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中展开相应数据库的“角色”，然后单击某个数据库角色（或创建一个新的数据库角色）。  
  
2.  在 **“常规”** 选项卡中，选择 **“读取定义”** 选项。  
  
3.  在“成员身份”  窗格中，输入使用此角色连接到 Analysis Services 的 Windows 用户和组帐户。  
  
4.  单击“确定”  ，完成角色创建。  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>设置单个对象的读取定义权限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，打开“数据库”文件夹，选择一个数据库，在对象资源管理器中展开相应数据库的“角色”，然后单击某个数据库角色（或创建新的数据库角色）。  
  
2.  在“常规”  窗格，为 **Read Definition**清除数据库权限。 此步骤清除了权限继承，这样便可对单个对象设置权限。  
  
3.  选择为其指定“读取定义”  属性的对象：  
  
    -   在“数据源”  窗格，为该数据源单击“读取定义”  复选框。 角色成员可查看数据源的连接字符串，包括服务器名称，还可能包括用户名称。 假如你想提供连接字符串信息，而不同时授予修改连接字符串或查看任何其它对象定义的权限，这时该权限可用。  
  
    -   在“维度”  窗格，为该维度单击“读取定义”  复选框。 有经验的分析人员和开发人员在没有能修改定义或查看其他对象（例如，其他维度、多维数据集对象或挖掘结构和模型）定义的权限的情况下，可能需要查看定义。  
  
    -   在“挖掘结构”窗格，单击数据挖掘结构或模型的“读取定义”  复选框。 浏览数据模型需要“读取定义” 。 有关详细信息，请参阅[授予数据挖掘结构和模型的权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)。  
  
4.  在“成员身份”  窗格中，输入使用此角色连接到 Analysis Services 的 Windows 用户和组帐户。  
  
5.  单击“确定”  ，完成角色创建。  
  
## <a name="see-also"></a>另请参阅  
 [授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [授予处理权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
