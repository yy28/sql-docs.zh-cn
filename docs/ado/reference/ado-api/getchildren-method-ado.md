---
title: "GetChildren 方法 (ADO) |Microsoft 文档"
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
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords: GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fff51cb110366031907d8aeaa272f72eb7dc0fd2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="getchildren-method-ado"></a>GetChildren 方法 (ADO)
返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)其行表示集合的子级[记录](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>返回值  
 A**记录集**每一行都表示当前的子对象**记录**对象。 例如的子级**记录**，表示一个目录将是文件和包含在父目录的子目录。  
  
## <a name="remarks"></a>Remarks  
 提供程序确定哪些列存在在返回**记录集**。 例如，文档源提供程序始终返回资源**记录集**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
