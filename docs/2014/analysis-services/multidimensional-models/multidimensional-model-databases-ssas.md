---
title: 多维模型数据库（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5da033881d2a993ea4be6674dcf8b228cad80bf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073521"
---
# <a name="multidimensional-model-databases-ssas"></a>多维模型数据库 (SSAS)
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库是数据源、数据源视图、多维数据集、维度以及角色的集合。 此外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库可以选择包含数据挖掘的结构以及一些自定义程序集，通过这些程序集，您可以将用户定义函数添加到数据库。  
  
 多维数据集是 Analysis Services 中的基本查询对象。 当通过客户端应用程序连接到 Analysis Services 数据库时，可以连接到该数据库中的多维数据集。 如果正在跨多个上下文重用维度、程序集、角色或挖掘结构，数据库可能包含多个多维数据集。  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以使用下列交互方式之一或以编程方式创建和修改  数据库：  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 项目从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署到指定的  实例。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如果该实例中没有同名的数据库，则此过程会创建  数据库，并在新创建的数据库中实例化已设计的对象。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时，仅当将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到  实例时，对此项目中的对象所做的更改才会生效。  
  
-   使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例中创建一个空的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]数据库，然后使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 直接连接到该数据库并在其中（而不是在项目中）创建对象。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 按此方式使用  数据库时，保存已更改的对象后，对对象所做的更改也会在要连接到的数据库中生效。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用与源代码管理软件集成来支持多个开发人员同时使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目中的不同对象。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 开发人员也可以与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库直接进行交互，而不通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，但是这样做的风险是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的对象可能会与用于其部署的  项目不同步。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署之后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来管理  数据库。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库（例如对分区和角色）进行某些更改，这些更改也可能会导致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的对象与用于其部署的  项目不同步。  
  
## <a name="related-tasks"></a>Related Tasks  
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)  
  
 [备份和还原 Analysis Services 数据库](backup-and-restore-of-analysis-services-databases.md)  
  
 [记录和编写 Analysis Services 数据库脚本](document-and-script-an-analysis-services-database.md)  
  
 [修改或删除 Analysis Services 数据库](modify-or-delete-an-analysis-services-database.md)  
  
 [移动 Analysis Services 数据库](move-an-analysis-services-database.md)  
  
 [重命名多维数据库 &#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md)  
  
 [设置多维数据库 &#40;Analysis Services 的兼容级别&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [设置多维数据库属性 &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)  
  
 [同步 Analysis Services 数据库](synchronize-analysis-services-databases.md)  
  
 [在 ReadOnly 和 ReadWrite 模式之间切换 Analysis Services 数据库](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>另请参阅  
 [以联机模式连接到 Analysis Services 数据库](connect-in-online-mode-to-an-analysis-services-database.md)   
 [&#40;SSDT 创建 Analysis Services 项目&#41;](create-an-analysis-services-project-ssdt.md)   
 [使用 MDX 查询多维数据](mdx/querying-multidimensional-data-with-mdx.md)  
  
  
