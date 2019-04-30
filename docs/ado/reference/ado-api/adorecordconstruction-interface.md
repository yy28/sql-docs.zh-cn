---
title: ADORecordConstruction 接口 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21975fb2442aea97e362cd71b24c087f58addc0f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248843"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 接口
**ADORecordConstruction**界面用于构造 ADO**记录**从 OLE DB 对象**行**C 中的对象 /C++应用程序。  
  
 此接口支持以下属性：  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|只写。<br />设置容器的 OLE DB**行**对象上此 ADO**记录**对象。|  
|[Row](../../../ado/reference/ado-api/row-property-ado.md)|读/写。<br />获取/设置 OLE DB**行**对象从/对此 ADO**记录**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>备注  
 提供 OLE DB**行**对象 (`pRow`)，ADO 构造**记录**对象 (`adoR`)，相当于以下三个基本操作：  
  
1.  创建 ADO**记录**对象：  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  查询**IADORecordConstruction**接口**记录**对象：  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  调用**IADORecordConstruction::put_Row**属性方法以设置 OLE DB**行**对象上 ADO**记录**对象：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 所产生的**adoR**对象现在表示 ADO**记录**构造从 OLE DB 对象**行**对象。  
  
 ADO**记录**还可以从 OLE DB 容器构造对象**行**对象。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 及更高版本  
  
 **库：** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
