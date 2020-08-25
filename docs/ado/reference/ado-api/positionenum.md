---
description: PositionEnum
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d7b443e94f3bea5977aeaf953e84c66c826daeb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773166"
---
# <a name="positionenum"></a>PositionEnum
指定记录指针在 [记录集中](./recordset-object-ado.md)的当前位置。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指示当前记录指针处于 BOF (也就是说， [bof](./bof-eof-properties-ado.md) 属性为 **True**) 。|  
|**adPosEOF**|-3|指示当前记录指针位于 EOF (即， [eof](./bof-eof-properties-ado.md) 属性为 **True**) 。|  
|**adPosUnknown**|-1|指示 **记录集** 为空，当前位置未知，或者提供程序不支持 [AbsolutePage](./absolutepage-property-ado.md) 或 [AbsolutePosition](./absoluteposition-property-ado.md) 属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums。未知|  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [AbsolutePage 属性 (ADO)](./absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [AbsolutePosition 属性 (ADO)](./absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::