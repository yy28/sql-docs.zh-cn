---
title: SeekEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25585f77de1e5a05051d4fad8e1cdca7ca1172c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="seekenum"></a>SeekEnum
指定的一种[Seek](../../../ado/reference/ado-api/seek-method.md)执行。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|查找第一个键等于*KeyValues*。|  
|**adSeekLastEQ**|2|查找等于的最后一个键*KeyValues*。|  
|**adSeekAfterEQ**|4|查找这两个密钥等于*KeyValues*或紧随其后将要发生匹配。|  
|**adSeekAfter**|8|紧随其后的位置查找某个键包含的匹配项*KeyValues*应发生。|  
|**adSeekBeforeEQ**|16|查找这两个密钥等于*KeyValues*或之前将要发生匹配。|  
|**adSeekBefore**|32|其中包含的匹配项之前查找密钥*KeyValues*应发生。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>适用范围  
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
