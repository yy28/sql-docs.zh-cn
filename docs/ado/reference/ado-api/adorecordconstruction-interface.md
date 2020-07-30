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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4dca796e9ba3c353d48fd3620c34a141c35a3fe8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242827"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 接口
**ADORecordConstruction**接口用于从 c/c + + 应用程序中的 OLE DB**行**对象构造 ADO**记录**对象。  
  
 此接口支持以下属性：  
  
## <a name="properties"></a>属性  
  
|属性|描述|  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|只写。<br />设置此 ADO**记录**对象上 OLE DB**行**对象的容器。|  
|[行](../../../ado/reference/ado-api/row-property-ado.md)|读/写。<br />获取/设置此 ADO**记录**对象的 OLE DB**行**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>备注  
 给定一个 OLE DB**行**对象（ `pRow` ），即 ADO **Record**对象（）的构造 `adoR` ，其中包含以下三个基本操作：  
  
1.  创建 ADO**记录**对象：  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  查询**Record**对象上的**IADORecordConstruction**接口：  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  调用**IADORecordConstruction：:p ut_Row**属性方法，在 ADO**记录**对象上设置 OLE DB**行**对象：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 生成的**adoR**对象现在表示从 OLE DB**行**对象构造的 ADO**记录**对象。  
  
 ADO**记录**对象还可以从 OLE DB**行**对象的容器构造。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 及更高版本  
  
 **库：** msado15.dll  
  
 **UUID：** 00000567-0000-0010-8000-00AA006D2EA4
