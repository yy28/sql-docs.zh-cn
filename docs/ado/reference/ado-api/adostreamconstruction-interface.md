---
title: ADOStreamConstruction 接口 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf21be88854837ab2dff1a8bc8bc73f44a6e20c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248831"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 接口
**ADOStreamConstruction**界面用于构造 ADO **Stream**从 OLE DB 对象**IStream** C 中的对象 /C++应用程序。  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[Stream 属性](../../../ado/reference/ado-api/stream-property.md)|读/写。 获取/设置 OLE DB **Stream**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>备注  
 提供 OLE DB **IStream**对象 (`pStream`)，ADO 构造**Stream**对象 (`adoStr`) 相当于以下三个基本操作：  
  
1.  创建 ADO **Stream**对象：  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  查询**IADOStreamConstruction**接口**Stream**对象：  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 调用`IADOStreamConstruction::get_Stream`属性方法以设置 OLE DB **IStream**对象上 ADO **Stream**对象：  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 所产生的`adoStr`对象现在表示 ADO **Stream**构造从 OLE DB 对象**IStream**对象。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 或更高版本  
  
 **库：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)
