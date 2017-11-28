---
title: "对象定义中表格模型脚本语言 (TMSL) |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 031c472ad444e809126eb897755777f970032b51
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="tmsl-reference---tabular-objects"></a>TMSL 引用的表格对象

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  应用程序的创建、 使用，或管理表格数据库或连接到的 SQL Sever 2016 Analysis Services 实例在表格模式下，可用于命令和 JSON 格式的对象表示形式的表格模型脚本语言 (TMSL)。  
  
 本文记录生成的 SQL Server Management Studio、 SQL Server Data Tools (SSDT) 和 AMO PowerShell 脚本中使用的 TMSL 架构的主要对象。  
  
 对象定义中 JSON 和如 Create、 Alter、 TMSL 命令中使用和删除。 请参阅[命令中表格模型脚本语言 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)有关命令的列表。  
  
## <a name="main-objects"></a>主要对象  
 下表是 TMSL 脚本中的最常用对象的列表。  
  
|||  
|-|-|  
|[数据库对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|定义表格数据库兼容级别 1200年或更高版本，基于相同级别的模型。|  
|[模型对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|定义在兼容级别 1200年或更高的表格模型。|  
|[数据源对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|到数据源时模型处于 DirectQuery 模式下使用导入模型中，加载过程中或传递查询中定义的连接。|  
|[Tables 对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|指定模型的表。|  
|[分区对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|定义的表行集合，包括计算的表的存储。|  
|[关系对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|定义表之间的关系。|  
|[角色对象 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|定义权限、 成员身份，以及控制访问权限的安全筛选器对数据和操作。|  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
