---
title: 对象定义中表格模型脚本语言 (TMSL) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de968c32f8c00132157a5b1b7a6682adc7148446
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851742"
---
# <a name="tmsl-reference---tabular-objects"></a>TMSL 引用 - 表格对象
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  应用程序的创建、 使用，或管理表格数据库或连接到 SQL Server 2016 Analysis Services 实例在表格模式下，可以使用表格模型脚本语言 (TMSL) 命令和 JSON 格式的对象表示形式。  
  
 本文介绍在 SQL Server Management Studio、 SQL Server Data Tools (SSDT) 和 AMO PowerShell 生成的脚本中使用的 TMSL 架构的主要对象。  
  
 对象定义中 JSON 和 TMSL 如 Create、 Alter 命令中使用和删除。 请参阅[表格模型脚本语言中的命令&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)有关的命令列表。  
  
## <a name="main-objects"></a>主要对象  
 下表是 TMSL 脚本中最常使用的对象的列表。  
  
|||  
|-|-|  
|[数据库对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|定义基于模型的相同级别的表格数据库的兼容性级别为 1200年或更高版本，概况。|  
|[模型对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|定义在兼容级别 1200年或更高的表格模型。|  
|[数据源对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|定义到数据源时在模型处于 DirectQuery 模式下使用要加载的模型，导入过程中或通过查询传递的连接。|  
|[Tables 对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|指定模型的表。|  
|[分区对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|定义的表行集，包括计算的表的存储。|  
|[关系对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|定义表之间的关系。|  
|[角色对象&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|定义权限、 成员资格，以及控制访问权限的安全筛选器对数据和操作。|  
  
## <a name="see-also"></a>请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
