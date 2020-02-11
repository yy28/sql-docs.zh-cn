---
title: ADCPROP_AUTORECALC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 738f4cece8cf2355c12c0de4ac42314152c6370a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921444"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
指定[MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)提供程序何时重新计算分层记录集中的聚合和计算列。  
  
 这些常量仅用于**MSDataShape**提供程序和**记录集**"**自动**重新计算" 动态属性，该属性在[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)中进行了引用，并在[Microsoft Cursor service for OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)或[microsoft 数据定形服务（用于 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)文档）中进行了介绍。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|默认值。 每当**MSDataShape**提供程序确定计算列所依赖的值已更改时重新计算。|  
|**adRecalcUpFront**|0|仅当最初生成分层**记录集**时才进行计算。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。
