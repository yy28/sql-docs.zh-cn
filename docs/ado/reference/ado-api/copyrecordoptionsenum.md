---
title: CopyRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a944d3f82940d9364312fb8033ec8b8937b0c49c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695765"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定的行为[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|指示*源*提供程序尝试模拟使用下载的副本并上传操作，如果此方法无法*目标*在另一台服务器上或由不同服务于访问接口*源*。 请注意，不同提供程序的功能可能会导致性能下降或丢失数据。|  
|**adCopyNonRecursive**|2|将当前目录，但无及其子目录复制到目标。 复制操作是非递归。|  
|**adCopyOverWrite**|1|如果将覆盖该文件或目录*目标*指向现有文件或目录。|  
|**adCopyUnspecified**|-1|默认值。 执行默认复制操作：如果目标文件或目录已存在，则操作将失败并操作副本以递归方式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
