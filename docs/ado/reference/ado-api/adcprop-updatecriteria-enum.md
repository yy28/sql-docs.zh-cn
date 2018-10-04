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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4d64095c02fbf3f969248fc78d375a191fe72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762728"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些字段可用于在具有的数据源的行中的开放式更新过程中检测冲突[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
 使用与这些常量**记录集**"**更新条件**"中引用的动态属性[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)记录[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文档。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果已更改的数据源行的任何列，检测冲突。|  
|**adCriteriaKey**|0|检测到冲突，如果源行中的键列的数据已更改，这意味着已删除行。|  
|**adCriteriaTimeStamp**|3|检测到冲突，如果源行数据的时间戳已更改，这意味着该行已被访问后**记录集**获取。|  
|**adCriteriaUpdCols**|2|检测到冲突的任何列的数据源的行，如果对应于已更新字段**记录集**已更改。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
