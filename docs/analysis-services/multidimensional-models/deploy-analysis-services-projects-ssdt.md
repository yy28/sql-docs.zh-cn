---
title: "部署 Analysis Services 项目 (SSDT) |Microsoft 文档"
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
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dbfe19ac5da2fee064dd19d06aa1bf7992c3429b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="deploy-analysis-services-projects-ssdt"></a>部署 Analysis Services 项目 (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中开发 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目时，应经常将项目部署到开发服务器以创建项目所定义的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 这是测试项目所必需的；例如，浏览多维数据集中的单元，浏览维度成员或验证关键绩效指标 (KPI) 公式。  
  
## <a name="deploying-a-project"></a>部署项目  
 您可以独立部署项目，也可以部署解决方案中的所有项目。 部署项目时，将按顺序执行数个操作。 首先，生成项目。 此步骤创建了定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库及其构成对象的输出文件。 接下来，验证目标服务器。 最后，在目标服务器上创建目标数据库及其对象。 除非在先前的部署过程中项目创建了这些对象，否则部署过程中，部署引擎会将预先存在的数据库完全替换为项目内容。  
  
 在初始部署之后, IncrementalSnapshot.xml 文件中将生成\<项目名称 > \obj 文件夹。 此文件用于确定目标服务器上的数据库或其对象是否已在项目外部进行了更改。 如果进行了更改，则系统将提示您覆盖目标数据库中的所有对象。 如果在项目中进行了所有更改并且将项目配置为增量部署，则仅将更改部署到目标服务器。  
  
 项目配置及其关联的设置确定将用于部署项目的部署属性。 对于共享项目，每个开发人员都可以将自己的配置用于自己的项目配置选项。 例如，每个开发人员都可以指定不同的测试服务器，以便将自己的工作与其他开发人员的工作区隔开来。  
  
## <a name="see-also"></a>另请参阅  
 [创建 Analysis Services 项目 &#40;SSDT &#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
