---
title: ADCPROP_UPDATECRITERIA_ENUM |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc5f18fbcff9b9681d95d4f8c9f0865b5eecace0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35275216"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些字段可用于在具有的数据源的行中的开放式更新过程中检测冲突[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
 使用与这些常量**记录集**"**更新条件**"动态属性，这在中引用[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)记录[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文档。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|@shouldalert|如果已更改的数据源行的任何列，检测到冲突。|  
|**adCriteriaKey**|0|检测到冲突，如果源行中的键列的数据已更改，这意味着已删除行。|  
|**adCriteriaTimeStamp**|3|检测到冲突，如果源行中的数据的时间戳已更改，这意味着该行已被访问后**记录集**获得。|  
|**adCriteriaUpdCols**|2|检测到冲突，如果任何数据源的列的行，对应于更新字段**记录集**已更改。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
