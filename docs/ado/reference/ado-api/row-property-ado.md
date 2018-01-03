---
title: "行属性 (ADO) |Microsoft 文档"
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
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords: Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed9e10206acfd86477a7f982676c1cb82711a1b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="row-property-ado"></a>行属性 (ADO)
获取或设置 OLE DB**行**对象或者[ADORecordConstruction 接口](../../../ado/reference/ado-api/adorecordconstruction-interface.md)对象。 当你使用**put_Row**设置**行**对象，行转换为 ADO**记录**对象。  
  
## <a name="readwritesyntax"></a>读/写。语法  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parameters  
 *ppRow*  
 指向 OLE DB**行**对象。  
  
 *PRow*  
 OLE DB**行**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值，包括，则为 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>适用范围  
 [ADORecordConstruction 接口](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
