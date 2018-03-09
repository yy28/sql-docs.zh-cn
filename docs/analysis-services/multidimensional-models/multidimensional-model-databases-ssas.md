---
title: "多维模型数据库 (SSAS) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
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
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 854371e81b8adf0ecf32c2685e64f5d136d00987
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="multidimensional-model-databases-ssas"></a>多维模型数据库 (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库是数据源、数据源视图、多维数据集、维度以及角色的集合。 此外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库可以选择包含数据挖掘的结构以及一些自定义程序集，通过这些程序集，您可以将用户定义函数添加到数据库。  
  
 多维数据集是 Analysis Services 中的基本查询对象。 当通过客户端应用程序连接到 Analysis Services 数据库时，可以连接到该数据库中的多维数据集。 如果正在跨多个上下文重用维度、程序集、角色或挖掘结构，数据库可能包含多个多维数据集。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以使用下列交互方式之一或以编程方式创建和修改  数据库：  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 项目从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署到指定的  实例。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如果该实例中没有同名的数据库，则此过程会创建  数据库，并在新创建的数据库中实例化已设计的对象。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时，仅当将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到  实例时，对此项目中的对象所做的更改才会生效。  
  
-   使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例中创建一个空的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]数据库，然后使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 直接连接到该数据库并在其中（而不是在项目中）创建对象。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 按此方式使用  数据库时，保存已更改的对象后，对对象所做的更改也会在要连接到的数据库中生效。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 通过与源代码管理软件集成来支持多个开发人员同时使用一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的不同对象。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 开发人员也可以与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库直接进行交互，而不通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，但是这样做的风险是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的对象可能会与用于其部署的  项目不同步。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署之后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来管理  数据库。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库（例如对分区和角色）进行某些更改，这些更改也可能会导致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的对象与用于其部署的  项目不同步。  
  
## <a name="related-tasks"></a>相关任务  
 [附加和分离 Analysis Services 数据库](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Document and Script Analysis Services 数据库](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [修改或删除 Analysis Services 数据库](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [移动 Analysis Services 数据库](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [重命名多维数据库 (Analysis Services)](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [设置多维数据库属性 (Analysis Services)](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>另请参阅  
 [在联机模式下连接到 Analysis Services 数据库](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [创建 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [使用 MDX 查询多维数据](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  
