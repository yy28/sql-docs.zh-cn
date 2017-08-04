---
title: "延隔时间 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAG
dev_langs:
- DMX
helpviewer_keywords:
- Lag function
ms.assetid: 2da6df1a-5506-4871-a0f0-83292f1df41e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4947b2f9a0dc89cd79923f2528ee21471ea9091e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前事例的日期与定型集的最近日期之间的时间段。  
  
## <a name="syntax"></a>语法  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>返回类型  
 整型类型的标量值。  
  
## <a name="remarks"></a>注释  
 如果**延隔时间**函数用于 KEY TIME 列所在的位置在嵌套表中的模型，该函数必须位于嵌套 select 语句。  
  
## <a name="examples"></a>示例  
 下面的示例返回用于模型定型的数据过去 12 个月内的用例。  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

