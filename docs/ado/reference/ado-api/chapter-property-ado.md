---
title: 章节属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2791bc1a89f8cec1362ab1f00c3be739f7d56b96
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920109"
---
# <a name="chapter-property-ado"></a>Chapter 属性 (ADO)
获取或设置[ADORecordsetConstruction 接口](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)对象上/上的 OLE DB**章节**对象。 使用**put_Chapter**设置**章节**对象时，会将行的子集转换为 ADO[记录集对象](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 这会设置**行集**对象的当前章节。 此属性是可读写的。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>parameters  
 *plChapter*  
 指向章节句柄的指针。  
  
 *LChapter*  
 章节的句柄。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回标准的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>应用于  
 [ADORecordsetConstruction 接口](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
