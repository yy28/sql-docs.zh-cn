---
title: Flush 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3d9ab76d2f2ed1a6f5dbeaf58be7d2f919acd3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932547"
---
# <a name="flush-method-ado"></a>Flush 方法 (ADO)
强制的内容[Stream](../../../ado/reference/ado-api/stream-object-ado.md) ADO 缓冲区使用的基础对象中的剩余**Stream**相关联。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>备注  
 可以使用此方法将发送到基础对象的流缓冲区的内容： 例如，节点或文件的源的 URL 表示**Stream**对象。 你想要确保所有的更改时，应调用此方法对的内容做出**Stream**已写入。 但是，与 ADO 一起它不是通常只需要调用**刷新**，如 ADO 持续刷新其缓冲区尽可能多地在后台。 内容将变为**Stream**自动进行，不缓存，直至**刷新**调用。  
  
 关闭**Stream**与[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法的内容刷新**Stream**自动; 有是无需显式调用**刷新**紧靠**关闭**。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
