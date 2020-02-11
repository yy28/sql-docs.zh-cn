---
title: SQL Server 2014 中不推荐使用的 Analysis Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04d12aab677e38d17d4e869e6885eb470854d824
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081922"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的 Analysis Services 功能
  本主题介绍 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中仍然可用但不推荐使用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 按照计划， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>SQL Server 的下一版本中不支持的功能  
 下一版 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将不再支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 请不要在新的开发工作中使用这些功能，并尽快修改当前还在使用这些功能的应用程序。  
  
|类别|不推荐使用的功能|替代功能|  
|--------------|------------------------|-----------------|  
|MDX 函数|CalculationPassValue 函数|无。 OLAP 引擎管理计算传递。 不再需要此函数。|  
|MDX 函数|CalculationCurrentPass 函数|无。 OLAP 引擎管理计算传递。 不再需要此函数。|  
|多维表达式 (MDX)|默认情况下，NON_EMPTY_BEHAVIOR 查询优化器提示已打开。|在未来版本中，NON_EMPTY_BEHAVIOR 查询优化器提示将默认为关闭。 如果使用不当，MDX 优化提示可能会产生不正确的结果。|  
|其他|CELL_EVALUATION_LIST 内部单元属性|最初提供了一个适用于单元格的计算公式的列表。 它在此版本的 Analysis Services 中为空白。  现在已在 MDX 脚本中指定了解决顺序。 有关详细信息，请参阅[理解传递顺序和求解次序 &#40;MDX&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|对象|COM 程序集|COM 程序集可能会造成安全风险。 将来版本中将删除对于 COM 程序集的支持。|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 未来版本中不支持的功能  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的下一版本仍支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能，但以后的版本将删除这些功能。 具体是哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本现在还未确定。  
  
|类别|不推荐使用的功能|替代功能|  
|--------------|------------------------|-----------------|  
|多维模型|远程分区|无。 改用本地分区。 有关详细信息，请参阅[创建和管理本地分区 &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md) 。|  
|多维模型|远程链接的度量值组|远程链接的度量值组是使用远程服务器上的数据源的链接度量值组。 将远程数据源用于链接的度量值组计划未来不再使用。<br /><br /> 此功能没有替代功能。 我们建议改用本地链接的度量值组。 有关详细信息，请参阅 [Linked Measure Groups](multidimensional-models/linked-measure-groups.md) 。|  
|多维模型|维度写回|无。 如果您需要写回功能，请使用分区写回。 有关详细信息，请参阅[设置分区写回](multidimensional-models/set-partition-writeback.md)。|  
|多维模型|链接的维度|无。 请考虑将维度复制到其他模型而非链接到另一模型中的某个维度。|  
|MDX|Non_Empty_Behavior 属性|无。 创建计算成员时，错误设置此属性会增加返回无效结果的可能性。 OLAP 引擎的近期优化改善了对稀疏数据集的操作，使得此属性的相关性更小。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 向后兼容性](analysis-services-backward-compatibility.md)   
 [SQL Server 2014 中废弃的 Analysis Services 功能](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  
