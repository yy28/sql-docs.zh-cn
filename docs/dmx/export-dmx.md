---
title: "导出 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: EXPORT
dev_langs: DMX
helpviewer_keywords:
- exporting mining models
- exporting mining structures
- mining structures [DMX], exporting
- EXPORT statement
ms.assetid: 97617071-e560-4080-81af-a80276fc0823
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9997c79cba1c9c87d91c3deb53bbdd56bc389353
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将服务器中的挖掘模型或挖掘结构对象提取到 Analysis Services 备份文件 (.abf) 中。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>参数  
 *对象类型*  
 要导出 （挖掘模型或挖掘结构） 的对象的可选类型。  
  
 *对象名称*  
 可选。 要导出的对象的名称。  
  
 *文件名*  
 要作为字符串导出的文件的名称和位置。  
  
## <a name="remarks"></a>注释  
 如果语句指定了挖掘模型，则结果文件也将包含关联的挖掘结构。 如果该语句指定**带有 WITH DEPENDENCIES**，处理 （例如，数据源和数据源视图） 的对象所需的所有对象都包含在.abf 文件。  
  
 你必须是数据库或服务器管理员联系以导出或导入对象从[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。  
  
## <a name="export-mining-structure-example"></a>导出挖掘结构示例  
 在下例中，将目标邮件和预测挖掘结构以及关联挖掘模型导出到一个特定的文件位置。 由于关联模型是 Market Basket 挖掘结构的一部分，所以该示例也将导出 Market Basket 结构。 将不导出市场篮挖掘结构的一部分，因为关联模型已导出使用可能存在的任何其他挖掘模型**挖掘模型**，而不**挖掘结构**。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>导出挖掘模型示例  
 在下例中，将关联挖掘模型导出到指定的文件位置。 因为该语句指定**带有 WITH DEPENDENCIES**，.abf 文件中也提供的数据源和数据源视图对象。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [导入 &#40; DMX &#41;](../dmx/import-dmx.md)   
 [导出和导入数据挖掘对象](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
