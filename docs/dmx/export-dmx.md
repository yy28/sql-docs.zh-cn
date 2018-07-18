---
title: 导出 (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb777a0de00596c99e22e514986cf3ec930ba0fd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991058"
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
 （可选） 若要导出 （挖掘模型或挖掘结构） 的对象类型。  
  
 *对象名称*  
 可选。 要导出的对象的名称。  
  
 *filename*  
 要作为字符串导出的文件的名称和位置。  
  
## <a name="remarks"></a>Remarks  
 如果语句指定了挖掘模型，则结果文件也将包含关联的挖掘结构。 如果该语句指定**带有 WITH DEPENDENCIES**，.abf 文件中包括处理的对象 （例如，数据源和数据源视图） 所需的所有对象。  
  
 您必须是数据库或服务器管理员联系以导出或导入对象从[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。  
  
## <a name="export-mining-structure-example"></a>导出挖掘结构示例  
 在下例中，将目标邮件和预测挖掘结构以及关联挖掘模型导出到一个特定的文件位置。 由于关联模型是 Market Basket 挖掘结构的一部分，所以该示例也将导出 Market Basket 结构。 可能存在，因为将不导出市场篮挖掘结构的一部分，因为关联模型使用导出的任何其他挖掘模型**挖掘模型**，而非**挖掘结构**。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>导出挖掘模型示例  
 在下例中，将关联挖掘模型导出到指定的文件位置。 因为该语句指定**带有 WITH DEPENDENCIES**，.abf 文件中还包括的数据源和数据源视图对象。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [导入&AMP;#40;DMX&AMP;#41;](../dmx/import-dmx.md)   
 [导出和导入数据挖掘对象](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
