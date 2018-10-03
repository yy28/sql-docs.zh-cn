---
title: GetChildren 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 910977912a23ee48f740afccdb58c6f82801f2a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784175"
---
# <a name="getchildren-method-ado"></a>GetChildren 方法 (ADO)
返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)其中的行表示集合的子级[记录](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>返回值  
 一个**记录集**对象，为其每个行表示的当前子**记录**对象。 例如的子级**记录**，表示一个目录将文件和包含在父目录的子目录。  
  
## <a name="remarks"></a>备注  
 提供程序会确定哪些列存在于返回**记录集**。 例如，文档源提供程序始终返回资源**记录集**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
