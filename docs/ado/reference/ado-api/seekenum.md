---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e044c4a2cda01fcc9cbba2667beaae75a12caf
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63459342"
---
# <a name="seekenum"></a>SeekEnum
指定的类型[Seek](../../../ado/reference/ado-api/seek-method.md)执行。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|查找与相等的第一个键*架构*。|  
|**adSeekLastEQ**|2|查找等于的最后一个键*架构*。|  
|**adSeekAfterEQ**|4|查找密钥等于*架构*或紧随其后将具有匹配的发生位置。|  
|**adSeekAfter**|8|紧靠在何处查找键的匹配*架构*本来将要发生。|  
|**adSeekBeforeEQ**|16|查找密钥等于*架构*或之前将具有匹配的发生位置。|  
|**adSeekBefore**|32|之前查找密钥，其中使用的匹配*架构*本来将要发生。|  
  
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
