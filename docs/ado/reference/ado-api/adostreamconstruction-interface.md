---
title: ADOStreamConstruction 接口 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0be1e9a290fc95303220c9a6c4b80df7e75e2905
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 接口
**ADOStreamConstruction**接口用于构造 ADO**流**从 OLE DB 对象**IStream** C/c + + 应用程序中的对象。  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[Stream 属性](../../../ado/reference/ado-api/stream-property.md)|读/写。 获取/设置 OLE DB**流**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>注释  
 提供 OLE DB **IStream**对象 (`pStream`)，构造的 ADO**流**对象 (`adoStr`) 都可对以下三个基本操作：  
  
1.  创建 ADO**流**对象：  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  查询**IADOStreamConstruction**接口**流**对象：  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 调用`IADOStreamConstruction::get_Stream`属性方法以设置 OLE DB **IStream**上 ADO 对象**流**对象：  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 所产生的`adoStr`对象现在表示 ADO**流**构造从 OLE DB 对象**IStream**对象。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 或更高版本  
  
 **库：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)
