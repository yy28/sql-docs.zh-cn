---
title: ADCPROP_UPDATECRITERIA_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: rothja
ms.author: jroth
ms.openlocfilehash: c68e0d7aa7cdbea80fe2ca2f0ff05ab77ea20b6e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760676"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些字段可用于在使用[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的数据源的行的开放式更新过程中检测冲突。  
  
 在[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)中引用的**记录集**"**更新条件**" 动态属性和[用于 OLE DB 文档的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)中介绍了这些常量。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果数据源行的任何列已更改，则检测冲突。|  
|**adCriteriaKey**|0|如果数据源行的键列已更改（这意味着行已删除），则检测冲突。|  
|**adCriteriaTimeStamp**|3|如果数据源行的时间戳已更改，这意味着在获取**记录集**后访问了行，则检测冲突。|  
|**adCriteriaUpdCols**|2|如果已更改与**记录集**的更新字段对应的数据源行中的任何列，则检测冲突。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
