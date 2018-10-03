---
title: Isolation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Isolation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Isolation element
ms.assetid: 28c98c6f-668e-4547-8d25-127cc3995a7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23abd455717c5eb6ae9e32c4ad9309e52f3841e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121357"
---
# <a name="isolation-element-assl"></a>Isolation 元素 (ASSL)
  指示派生自的元素的隔离级别[数据源](../data-type/datasource-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ReadCommitted*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../data-type/datasource-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*ReadCommitted*|指定语句不能读取已由其他事务修改但尚未提交的数据。 这样可以避免脏读。 其他事务可以在当前事务的各个语句之间更改数据。 这将导致不可重复读取和虚拟数据。 此值是 `Isolation` 元素的默认值。|  
|*快照*|指定事务中任何语句读取的数据都将是在事务开始时便存在的数据的事务性一致版本。 事务只能查看在其开始之前提交的数据修改。 对于正在当前事务中执行的语句，其他事务在当前事务开始后所做的数据修改将不可见。 其效果就好像事务中的语句获得了已提交数据的快照，因为该数据在事务开始时就存在。|  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
