---
title: 行属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 041356f05daaaef50e6e81d995209ab5379fc901
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747405"
---
# <a name="row-property-ado"></a>Row 属性 (ADO)
获取或设置 OLE DB**行**对象或从[ADORecordConstruction 接口](../../../ado/reference/ado-api/adorecordconstruction-interface.md)对象。 当你使用**put_Row**若要设置**行**对象，一行转换为 ADO**记录**对象。  
  
## <a name="readwritesyntax"></a>读/写。语法  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parameters  
 *ppRow*  
 指向 OLE DB**行**对象。  
  
 *pRow*  
 OLE DB**行**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值，包括，则为 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>适用范围  
 [ADORecordConstruction 接口](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
