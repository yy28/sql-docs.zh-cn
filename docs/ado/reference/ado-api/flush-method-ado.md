---
title: Flush 方法（ADO） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932547"
---
# <a name="flush-method-ado"></a>Flush 方法 (ADO)
将 ADO 缓冲区中的[流](../../../ado/reference/ado-api/stream-object-ado.md)的内容强制转换为与**流**关联的基础对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>备注  
 此方法可用于将流缓冲区的内容发送到基础对象：例如，作为**流**对象的源的 URL 所表示的节点或文件。 若要确保已写入对**流**内容所做的所有更改，应调用此方法。 但是，在 ADO 中，通常不需要调用**Flush**，因为 ADO 会在后台持续刷新其缓冲区。 对**流**内容所做的更改将自动进行，而不会在调用**刷新**之前缓存。  
  
 使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法关闭**流**会自动刷新**流**的内容;不需要在**关闭**前显式调用**刷新**。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
