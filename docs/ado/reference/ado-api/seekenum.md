---
title: "SeekEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: SeekEnum
helpviewer_keywords: SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6f60ed06b2f23bceec62822f43b77f5c10c3ce1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="seekenum"></a>SeekEnum
指定的一种[Seek](../../../ado/reference/ado-api/seek-method.md)执行。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|@shouldalert|查找第一个键等于*KeyValues*。|  
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
