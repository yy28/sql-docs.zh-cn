---
title: 数据源来自现有对象 （数据源向导） (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourcewizard.specifyobject.f1
ms.assetid: e6ef6dea-9db8-45c4-8959-f9febd7caf7b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90773f9a7ccf7e1e34cc81f761b7a9849144d4a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142237"
---
# <a name="data-sources-from-existing-objects-data-source-wizard-analysis-services"></a>来自现有对象的数据源（数据源向导）(Analysis Services)
  可以使用 **“来自现有对象的数据源”** 页，指定新数据源基于的现有数据源或项目。  
  
## <a name="options"></a>选项  
 **创建基于解决方案中的现有数据源的数据源**  
 选择此选项可基于解决方案中的现有数据源创建新的数据源。 在生成、刷新或部署使用新数据源的项目时，新数据源将从您在选择此选项时指定的数据源获取设置。  
  
 **数据源**  
 从按项目分组的数据源列表中，选择希望新数据源基于的数据源。  
  
 **创建数据源基于 Analysis Services 项目**  
 选择此选项可创建引用当前解决方案中另一个 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的新数据源。 新数据源将从所选项目的 `TargetServer` 和 `TargetDatabase` 属性获取设置。 在生成、刷新或部署使用新数据源的项目时，新数据源将从您在选择此选项时指定的数据源获取设置。  
  
 **项目**  
 选择希望在新数据源中引用的项目。  
  
## <a name="see-also"></a>请参阅  
 [数据源向导的 F1 帮助&#40;Analysis Services&#41;](data-source-wizard-f1-help-analysis-services.md)   
 [多维模型中的数据源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支持的数据源&#40;SSAS 多维&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
