---
title: 主题区域数据库架构选项 （架构生成向导） (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ce756687e73e628d1b66a797e19711a3d6889eec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014618"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>主题区域数据库架构选项（架构生成向导）（Analysis Services - 多维数据）
  可以使用 **“主题区域数据库架构选项”** 页，控制如何生成架构以及定义如何保留数据。  
  
## <a name="options"></a>“常规”  
 **所属架构**  
 指定新主题区域数据库中的架构的名称。  
  
 **在维度表上创建主键**  
 在生成的架构中为维度表创建主键。 如果不选择此选项，则不会生成任何索引。  
  
> [!NOTE]  
>  如果不选择此选项，将强制引用完整性。  
  
 **创建索引**  
 在生成的架构中为外键列创建索引。  
  
 **强制引用完整性**  
 在生成的架构中强制引用完整性。 如果不选择此选项，将创建关系但不会强制执行。  
  
 **保留重新生成数据**  
 向导完成时，在主题区域数据库中保留数据。 如果不选择此选项，则可能在无警告的情况下清除主题区域数据库中的所有数据。  
  
 **填充时间表**  
 指定向导如何填充时间表。 下表对此选项的可能值进行了说明：  
  
> [!NOTE]  
>  只有在项目模式下使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 从 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 项目调用架构生成向导时，才会启用此选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|填充|填充主题区域时间表。|  
|不填充|不填充主题区域时间表。|  
|为空时才填充|只有当主题区域时间表为空时才进行填充。|  
  
## <a name="see-also"></a>请参阅  
 [架构生成向导的 F1 帮助&#40;Analysis Services-多维数据&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  