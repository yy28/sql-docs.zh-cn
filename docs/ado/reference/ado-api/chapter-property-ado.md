---
description: Chapter 属性 (ADO)
title: ADO)  (的章节属性 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 04469dc7cc888a167135ad18a77469200614e925
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776296"
---
# <a name="chapter-property-ado"></a>Chapter 属性 (ADO)
获取或设置[ADORecordsetConstruction 接口](./adorecordsetconstruction-interface.md)对象上/上的 OLE DB**章节**对象。 使用 **put_Chapter** 设置 **章节** 对象时，会将行的子集转换为 ADO [记录集对象](./recordset-object-ado.md) 对象。 这会设置 **行集**对象的当前章节。 此属性是可读写的。  
  
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
  
## <a name="applies-to"></a>适用于  
 [ADORecordsetConstruction 接口](./adorecordsetconstruction-interface.md)