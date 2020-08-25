---
description: RowPosition 属性 (ADO)
title: " (ADO) 的 RowPosition 属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f5f78843e38c2a3ff6b21c90bc9ed7f2c573ee4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777606"
---
# <a name="rowposition-property-ado"></a>RowPosition 属性 (ADO)
获取或设置**ADORecordsetConstruction**对象上/的 OLE DB **RowPosition**对象。 使用 **put_RowPosition** 设置 **RowPosition** 对象时，生成的 **Recordset** 对象将使用 **RowPosition** 对象来确定当前行。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>parameters  
 *ppRowPos*  
 指向 OLE DB **RowPosition** 对象的指针。  
  
 *PRowPos*  
 OLE DB **RowPosition** 对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回标准的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="remarks"></a>备注  
 设置此属性时，如果**RowPosition**对象上的**行集**对象与**Recordset**对象上的**行**集对象不同，则前者会重写后者。 同样的行为也适用于**RowPosition**的当前**章节**。  
  
## <a name="applies-to"></a>适用于  
 [ADORecordsetConstruction 接口](./adorecordsetconstruction-interface.md)