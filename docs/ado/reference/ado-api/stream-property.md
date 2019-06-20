---
title: Stream 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0fecd8a1bfed75bd922ed39bd57144b9f32b6bb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710737"
---
# <a name="stream-property"></a>Stream 属性
获取或设置 OLE DB **Stream**对象从/上**ADOStreamConstruction**对象。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parameters  
 *ppStream*  
 指向 OLE DB **Stream**对象。  
  
 *pStream*  
 OLE DB **Stream**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值。 这包括，则为 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>适用范围  
 [ADOStreamConstruction 接口](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
