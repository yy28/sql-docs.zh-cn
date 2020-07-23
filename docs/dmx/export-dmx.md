---
title: 导出（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 620bb13d50461e850cc08de1e1b1b71709d78c7c
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971725"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  将服务器中的挖掘模型或挖掘结构对象提取到 Analysis Services 备份文件 (.abf) 中。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>参数  
 *对象类型*  
 可选。要导出的对象的类型（挖掘模型或挖掘结构）。  
  
 *对象名称*  
 可选。 要导出的对象的名称。  
  
 *filename*  
 要作为字符串导出的文件的名称和位置。  
  
## <a name="remarks"></a>备注  
 如果语句指定了挖掘模型，则结果文件也将包含关联的挖掘结构。 如果语句指定**具有依赖项**，则处理对象所需的所有对象（例如，数据源和数据源视图）都包含在 .abf 文件中。  
  
 您必须是数据库或服务器管理员才能从数据库中导出或导入对象 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
## <a name="export-mining-structure-example"></a>导出挖掘结构示例  
 在下例中，将目标邮件和预测挖掘结构以及关联挖掘模型导出到一个特定的文件位置。 由于关联模型是 Market Basket 挖掘结构的一部分，所以该示例也将导出 Market Basket 结构。 由于关联模型是使用**挖掘模型**而不是**挖掘结构**导出的，因此不会导出任何其他可能作为市场篮挖掘结构一部分存在的挖掘模型。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>导出挖掘模型示例  
 在下例中，将关联挖掘模型导出到指定的文件位置。 由于语句指定**了依赖项**，因此，数据源和数据源视图对象也包含在 .abf 文件中。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [导入 &#40;DMX&#41;](../dmx/import-dmx.md)   
 [导出和导入数据挖掘对象](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
