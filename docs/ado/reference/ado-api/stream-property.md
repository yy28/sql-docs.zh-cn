---
title: "流属性 |Microsoft 文档"
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
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6ee0a6a3827d0f2d3c7b7bf781f7fc1fd73a765
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="stream-property"></a>流属性
获取或设置 OLE DB**流**对象从/上**ADOStreamConstruction**对象。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parameters  
 *ppStream*  
 指向 OLE DB**流**对象。  
  
 *pStream*  
 OLE DB**流**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值。 这包括，则为 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>适用范围  
 [ADOStreamConstruction 接口](../../../ado/reference/ado-api/adostreamconstruction-interface.md)

