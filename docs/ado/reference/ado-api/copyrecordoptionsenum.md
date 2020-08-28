---
description: CopyRecordOptionsEnum
title: CopyRecordOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1570b0baa22b6d08db9b47d99f4d1e01595622d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974538"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定 [CopyRecord](./copyrecord-method-ado.md) 方法的行为。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|指示在以下情况下， *源* 提供程序将尝试使用下载和上载操作来模拟副本：由于 *目标*位于其他服务器上，或由不同于 *源*的提供程序提供服务。 请注意，不同的提供程序功能可能会影响性能或丢失数据。|  
|**adCopyNonRecursive**|2|将当前目录（但不是其任何子目录）复制到目标。 复制操作不是递归的。|  
|**adCopyOverWrite**|1|如果 *目标* 指向现有文件或目录，则覆盖文件或目录。|  
|**adCopyUnspecified**|-1|默认。 执行默认复制操作：如果目标文件或目录已存在，则操作将失败，并且操作将以递归方式进行复制。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [CopyRecord 方法 (ADO)](./copyrecord-method-ado.md)