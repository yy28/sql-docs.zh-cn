---
title: "SaveOptionsEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97f3d76d9fed33de5ba79d84a062891316c70ae0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定是否应创建或覆盖时从保存文件[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。 值可以是**adSaveCreateNotExist**或**adSaveCreateOverWrite**...  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|默认值。 如果指定的文件创建一个新文件*FileName*参数尚不存在。|  
|**adSaveCreateOverWrite**|2|中当前打开的数据将覆盖该文件**流**对象，如果指定的文件*Filename*参数已存在。 如果指定的文件*Filename*参数不存在，则创建新的文件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)

