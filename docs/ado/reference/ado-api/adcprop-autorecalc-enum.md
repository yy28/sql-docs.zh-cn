---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: c3c085a09b800bb5dd6ce02ca3fa2d570b74190e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718579"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
指定何时[MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)提供程序重新计算分层记录集中的聚合和计算列。  
  
 仅用于这些常量**MSDataShape**提供程序和**记录集**"**自动重新计算**"中引用的动态属性[ADO动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)并在有案可稽[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)或[Microsoft Data Shaping 服务适用于 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)文档。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|默认值。 每当重新计算**MSDataShape**提供程序确定取决于计算的列的值已更改。|  
|**adRecalcUpFront**|0|仅在最初生成层次结构时计算**记录集**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。
