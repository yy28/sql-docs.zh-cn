---
description: ADCPROP_AUTORECALC_ENUM
title: ADCPROP_AUTORECALC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 571d3eb0d8d836a96b2f3f7a79807bd2d2c16fdf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976838"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
指定 [MSDataShape](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 提供程序何时重新计算分层记录集中的聚合和计算列。  
  
 这些常量仅用于 **MSDataShape** 提供程序和 **记录集** "**自动**重新计算" 动态属性，该属性在 [ADO 动态属性索引](./ado-dynamic-property-index.md) 中进行了引用，并在 [Microsoft Cursor service for OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 或 [microsoft 数据定形服务（用于 OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 文档）中进行了介绍。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|默认。 每当 **MSDataShape** 提供程序确定计算列所依赖的值已更改时重新计算。|  
|**adRecalcUpFront**|0|仅当最初生成分层 **记录集**时才进行计算。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。