---
title: ADORecordsetConstruction 接口 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f08d007395c85ef6b423c7db6c1aed5b39cb27ca
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718546"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 接口
**ADORecordsetConstruction**界面用于构造 ADO**记录集**从 OLE DB 对象**行集**C 中的对象 /C++应用程序。  
  
 此接口支持以下属性：  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[一章](../../../ado/reference/ado-api/chapter-property-ado.md)|读/写。<br />获取/设置 OLE DB**章**对象从/对此 ADO**记录集**对象。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|读/写。<br />获取/设置 OLE DB **RowPosition**对象从/对此 ADO**记录集**对象。|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|读/写。<br />获取/设置 OLE DB**行集**对象从/对此 ADO**记录集**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>备注  
 提供 OLE DB**行集**对象 (`pRowset`)，ADO 构造**记录集**对象 (`adoRs`) 相当于以下三个基本操作：  
  
1.  创建 ADO**记录集**对象：  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  查询**IADORecordsetConstruction**接口**记录集**对象：  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  调用`IADORecordsetConstruction::put_Rowset`属性方法以设置 OLE DB`Rowset`上 ADO 对象`Recordset`对象：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 所产生的`adoRs`对象现在表示 ADO**记录集**构造从 OLE DB 对象**行集**对象。  
  
 您还可以构造 ADO**记录集**对象从 OLE DB**章**或**RowPosition**对象。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 及更高版本  
  
 **库：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>请参阅  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 属性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
