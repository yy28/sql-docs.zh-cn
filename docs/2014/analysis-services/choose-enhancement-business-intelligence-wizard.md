---
title: 选择增强功能 （商业智能向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35634d3094647cd7698ec1961b94cb2b6b5744e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243977"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>选择增强功能（商业智能向导）
  可以使用 **“选择增强功能”** 页选择商业智能增强功能，以添加到您的多维数据集或维度中。  
  
## <a name="options"></a>“常规”  
 **可用增强功能**  
 选择要添加的商业智能增强功能。 下表列出了可用的增强功能：  
  
|增强功能|Description|  
|-----------------|-----------------|  
|**定义时间智能**|为所选的层次结构添加其他时间视图。 这些视图包括“本期截止到现在”、“移动平均”和“期间到期间”。<br /><br /> 注意：此选项仅适用于多维数据集。|  
|**定义帐户智能**|向具有某一帐户属性的成员分配标准的会计分类，如收入和支出。<br /><br /> 如果度量值的聚合函数设置为 ByAccount，则 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例将使用会计分类来聚合帐户属性一段时间内所有成员的度量值。|  
|**定义维度智能**|使用维度智能可以指定维度的标准业务类型以及维度属性的有效类型。 客户端应用程序在分析数据时可以使用这些指定的类型。|  
|**指定一元运算符**|指定一元运算符，以替换与多维数据集中所包含父子层次结构的成员相关联的默认聚合。<br /><br /> 注意：此选项仅适用于多维数据集。|  
|**创建自定义成员公式**|创建自定义成员公式，以替换与带有不同运算符的维度成员相关联的默认聚合。|  
|**指定属性顺序**|指定如何排列所选属性的成员的顺序。 成员可以按所选属性的名称或键排列，也可以按与所选属性相关的属性的名称或键排列。 默认情况下，成员按所选属性的名称排列。|  
|**启用维度写回**|启用手动修改维度结构。 对允许写维度的更新直接记录在该维度表中。|  
|**定义半累加性行为**|手动定义帐户类型属性的各个度量值或成员的聚合方法。 如果多维数据集包含帐户维度，则可以使用“定义帐户智能”选项根据帐户类型自动设置半累加行为。<br /><br /> 注意：此选项仅适用于多维数据集。|  
|**定义货币换算**|定义换算和分析多维数据集中跨国数据的规则。 换算规则将应用于使用多维表达式 (MDX) 脚本（由商业智能向导生成）的多维数据集中。<br /><br /> 注意：此选项仅适用于多维数据集。|  
  
 **Description**  
 提供了所选商业智能增强功能的简要说明。  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
