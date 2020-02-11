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
ms.openlocfilehash: 58bbbc299f13c0d876807476136cede76894bbb8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916700"
---
# <a name="stream-property"></a>Stream 属性
获取或设置**ADOStreamConstruction**对象上/的 OLE DB**流**对象。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>parameters  
 *ppStream*  
 指向 OLE DB**流**对象的指针。  
  
 *pStream*  
 一个 OLE DB 的**流**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回标准的 HRESULT 值。 这包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>应用于  
 [ADOStreamConstruction 接口](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
