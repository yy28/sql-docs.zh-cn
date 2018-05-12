---
title: 使用 Analysis Services 项目和在开发过程中的数据库 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 018f937ed07c202aad17d5e7758f41a3082c4870
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="work-with-analysis-services-projects-and-databases-in-development"></a>使用 Analysis Services 项目和在开发过程中的数据库
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以在项目模式或联机模式下使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 开发 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库。  
  
## <a name="single-developer"></a>一个开发人员  
 如果只有一个开发人员开发整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库及其所有构成对象，则在商业智能解决方案生命周期中，开发人员可以随时在项目模式或联机模式下使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。 在一个开发人员进行开发的情况下，模式的选择不是特别重要。 维护与源代码管理系统集成的离线项目文件有许多优点，例如存档和回滚。 但是，对于一个开发人员，就不存在与其他开发人员交流更改的问题。  
  
## <a name="multiple-developers"></a>多个开发人员  
 多个开发人员使用商业智能解决方案时，在多数情况下（如果不是全部情况的话），要是开发人员不在项目模式下使用源代码管理进行工作，则将出现问题。 源代码管理可确保两个开发人员不会同时对同一对象进行更改。  
  
 例如，假设一个开发人员在项目模式下工作，并且对所选对象进行更改。 在该开发人员进行这些更改时，假设另一个开发人员在联机模式下对已部署的数据库进行更改。 当第一个开发人员尝试部署他或她的已修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，将出现问题。 也就是说， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将检测到，在已部署的数据库中这些对象已被更改，并提示此开发人员覆盖整个数据库，从而覆盖第二个开发人员所做的更改。 因为 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 无法解决 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目对象之间即将覆盖的更改，所以，第一个开发人员唯一的实际选择就是必须放弃他或她的所有更改，并基于当前版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库重新开始新的项目。  
  
  
