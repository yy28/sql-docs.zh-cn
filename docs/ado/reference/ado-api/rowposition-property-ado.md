---
title: RowPosition 属性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fad2ee85ef40431a6a4e16814f4711404c851d3f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711456"
---
# <a name="rowposition-property-ado"></a>RowPosition 属性 (ADO)
获取或设置 OLE DB **RowPosition**对象从/上**ADORecordsetConstruction**对象。 当你使用**put_RowPosition**若要设置**RowPosition**生成的对象**记录集**对象使用**RowPosition**对象传递给确定当前行。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parameters  
 *ppRowPos*  
 指向 OLE DB **RowPosition**对象。  
  
 *PRowPos*  
 OLE DB **RowPosition**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值，包括，则为 S_OK 和 E_FAIL。  
  
## <a name="remarks"></a>备注  
 设置此属性时，如果**行集**对象上**RowPosition**对象是从不同**行集**对象上**记录集**对象，前者将覆盖后者。 相同的行为适用于当前**章**的**RowPosition**也。  
  
## <a name="applies-to"></a>适用范围  
 [ADORecordsetConstruction 接口](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
