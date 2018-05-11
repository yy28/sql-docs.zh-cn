---
title: Isolation 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 24b49454bab6d13f9acc32d85295057535264c4b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="isolation-element-assl"></a>Isolation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  该值指示元素派生自的隔离级别[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ReadCommitted*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*ReadCommitted*|指定语句不能读取已由其他事务修改但尚未提交的数据。 这样可以避免脏读。 其他事务可以在当前事务的各个语句之间更改数据。 这将导致不可重复读取和虚拟数据。 此值是 **Isolation** 元素的默认值。|  
|*快照*|指定事务中任何语句读取的数据都将是在事务开始时便存在的数据的事务性一致版本。 事务只能查看在其开始之前提交的数据修改。 对于正在当前事务中执行的语句，其他事务在当前事务开始后所做的数据修改将不可见。 其效果就好像事务中的语句获得了已提交数据的快照，因为该数据在事务开始时就存在。|  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
