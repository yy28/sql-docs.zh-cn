---
title: "修改或删除 Analysis Services 数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 65f53460a5a967744e23895b965bda0c9501f8cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="modify-or-delete-an-analysis-services-database"></a>修改或删除 Analysis Services 数据库
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中部署之前以及在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中部署之后，可以更改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]数据库的名称和说明。 您还可以调整 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库上的其他设置，这取决于环境。  
  
> [!NOTE]  
>  您不能在联机模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 更改数据库属性。  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 修改数据库  
 一旦 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的部署完成，您就可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来更改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在连接到该数据库包含的数据源时使用的模拟模式。 模拟模式允许您指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在试图连接到某个数据源进行处理、浏览或钻取时使用的安全上下文。  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 修改数据库  
 您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 在项目模式下修改用于定义数据库的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的标题和说明的翻译。 有关在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中使用翻译的详细信息，请参阅 [Analysis Services 的全球化方案](../../analysis-services/globalization-scenarios-for-analysis-services.md)。  
  
 您还可以设置与由数据库中包含的维度的帐户属性使用的帐户类型相关联的别名和聚合函数。 别名允许您为帐户图表中的帐户类型选择您的组织使用的特定于业务的术语。 帐户属性的成员使用帐户类型来指示如何使用为数据库中包含的各个帐户类型指定的聚合函数来针对各个成员聚合度量值。 有关帐户属性的详细信息，请参阅 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="deleting-databases"></a>删除数据库  
 删除某个现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库将删除该数据库和该数据库中所有的多维数据集、维度和挖掘模型。 您只能在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中删除现有的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]数据库。  
  
#### <a name="to-delete-an-analysis-services-database"></a>删除 Analysis Services 数据库  
  
1.  连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
2.  **“对象资源管理器”**中，展开连接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的节点，并确保要删除的对象可见。  
  
3.  右键单击要删除的对象，再选择“删除”。  
  
4.  在 **“删除对象”** 对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [记录和编写 Analysis Services 数据库脚本](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  
