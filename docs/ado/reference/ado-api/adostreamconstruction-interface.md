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
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920789"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 接口
**ADOStreamConstruction**接口用于从 c/c + + 应用程序中的 OLE DB **ISTREAM**对象构造 ADO**流**对象。  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[Stream 属性](../../../ado/reference/ado-api/stream-property.md)|读/写。 获取/设置 OLE DB**流**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>备注  
 给定一个 OLE DB **IStream**对象（`pStream`），将 ADO**流**对象（`adoStr`）的构造分为以下三个基本操作：  
  
1.  创建 ADO**流**对象：  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  查询**Stream**对象上的**IADOStreamConstruction**接口：  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 调用`IADOStreamConstruction::get_Stream`属性方法，设置 ADO**流**对象上的 OLE DB **IStream**对象：  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 生成`adoStr`的对象现在表示从 OLE DB **IStream**对象构造的 ADO**流**对象。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 或更高版本  
  
 **库：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另请参阅  
 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)
