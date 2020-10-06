---
description: SELECT INTO (DMX)
title: 选择 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 062e95b2030b3f4e3004fa1409f26fe82e38e05d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726107"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  创建新的挖掘模型，该挖掘模型是根据现有挖掘模型的挖掘结构生成的。 **SELECT INTO**语句通过复制架构和其他不特定于实际算法的信息来创建新的挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>参数  
 *新模型*  
 要创建的新模型的唯一名称。  
  
 *算法*  
 提供程序定义的数据挖掘算法的名称。  
  
 *参数列表*  
 可选。 由提供程序定义的算法所需参数的逗号分隔列表。  
  
 *expression*  
 计算结果为定型数据的有效筛选条件的表达式。 有关可用作筛选器的表达式的详细信息，请参阅 [Analysis Services 数据挖掘&#41;&#40;挖掘模型的筛选器 ](/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)。  
  
 *现有模型*  
 要复制的现有模型的名称。  
  
## <a name="remarks"></a>备注  
 如果现有模型已定型，则此语句执行时将自动处理新模型。 否则，新模型将保持未处理状态。  
  
 **SELECT INTO**语句仅在现有模型的结构与新模型的算法兼容时才起作用。 因此，此语句在快速创建并测试基于同一算法的模型时最为有用。 如果更改算法类型，则新算法必须支持现有模型中所有列的数据类型，否则处理模型时可能会出错。  
  
 **WITH 钻取**子句对新挖掘模型启用钻取功能。 只有在创建模型时，才能启用钻取功能。  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>示例 1：更改模型参数  
 下面的示例基于 `TM_Clustering` 您在 [数据挖掘基础教程](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))中创建的现有挖掘模型创建新的挖掘模型。 在新模型中，对 CLUSTER_COUNT 参数进行了修改；因而，新模型中的最大分类数为 5。 而现有模型使用的是默认值 10。  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>示例 2：向模型中添加筛选器  
 下面的示例基于现有挖掘模型创建一个新挖掘模型，并向其中添加了一个筛选器。 筛选器将定型数据限制为居住在特定区域的客户。  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  如此示例中所示，可通过使用 SELECT INTO 语句来更改应用于事例表的筛选器；但是，如果原始模型包含嵌套表的筛选器，则就不能使用此语法来更改或删除嵌套表筛选器，但可以从原始模型中原样复制该筛选器。 若要创建具有不同嵌套表筛选器的模型，请使用 ALTER STRTUCTURE...ADD MODEL 语法。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
