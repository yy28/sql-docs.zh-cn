---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf0c00fb7f353171686f57405879b3beb544aa1d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些字段可用于在具有的数据源的行中的开放式更新过程中检测冲突[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
 使用与这些常量**记录集**"**更新条件**"动态属性，这在中引用[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)记录[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文档。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果已更改的数据源行的任何列，检测到冲突。|  
|**adCriteriaKey**|0|检测到冲突，如果源行中的键列的数据已更改，这意味着已删除行。|  
|**adCriteriaTimeStamp**|3|检测到冲突，如果源行中的数据的时间戳已更改，这意味着该行已被访问后**记录集**获得。|  
|**adCriteriaUpdCols**|2|检测到冲突，如果任何数据源的列的行，对应于更新字段**记录集**已更改。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package: **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
