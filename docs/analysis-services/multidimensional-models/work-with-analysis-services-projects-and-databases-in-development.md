---
title: "使用 Analysis Services 项目和在开发过程中的数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c46155050b4772414f2f5e0d706cbca7dd1740db
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="work-with-analysis-services-projects-and-databases-in-development"></a>使用 Analysis Services 项目和在开发过程中的数据库
  可以在项目模式或联机模式下使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 开发 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库。  
  
## <a name="single-developer"></a>一个开发人员  
 如果只有一个开发人员开发整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库及其所有构成对象，则在商业智能解决方案生命周期中，开发人员可以随时在项目模式或联机模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。 在一个开发人员进行开发的情况下，模式的选择不是特别重要。 维护与源代码管理系统集成的离线项目文件有许多优点，例如存档和回滚。 但是，对于一个开发人员，就不存在与其他开发人员交流更改的问题。  
  
## <a name="multiple-developers"></a>多个开发人员  
 多个开发人员使用商业智能解决方案时，在多数情况下（如果不是全部情况的话），要是开发人员不在项目模式下使用源代码管理进行工作，则将出现问题。 源代码管理可确保两个开发人员不会同时对同一对象进行更改。  
  
 例如，假设一个开发人员在项目模式下工作，并且对所选对象进行更改。 在该开发人员进行这些更改时，假设另一个开发人员在联机模式下对已部署的数据库进行更改。 当第一个开发人员尝试部署他或她的已修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，将出现问题。 也就是说， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将检测到，在已部署的数据库中这些对象已被更改，并提示此开发人员覆盖整个数据库，从而覆盖第二个开发人员所做的更改。 因为 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 无法解决 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象之间即将覆盖的更改，所以，第一个开发人员唯一的实际选择就是必须放弃他或她的所有更改，并基于当前版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库重新开始新的项目。  
  
  

