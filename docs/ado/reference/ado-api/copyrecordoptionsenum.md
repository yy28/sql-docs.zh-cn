---
title: "CopyRecordOptionsEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e747e5bb2bcff9a8e414d809c127df09c251afa4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定的行为[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|指示*源*提供程序尝试模拟副本使用下载和上载操作，如果此方法失败由于*目标*正在不同的服务器上或通过其他服务提供程序比*源*。 请注意，不同提供程序功能可能会导致性能下降，或者会丢失数据。|  
|**adCopyNonRecursive**|2|将当前目录中，但不及其子目录复制到目标。 复制操作不是递归的。|  
|**adCopyOverWrite**|1|如果将覆盖文件或目录*目标*指向现有文件或目录。|  
|**adCopyUnspecified**|-1|默认值。 执行默认复制操作： 如果目标文件或目录已存在，则操作将失败并操作副本以递归方式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)

