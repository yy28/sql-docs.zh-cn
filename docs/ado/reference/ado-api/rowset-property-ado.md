---
title: 行集属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 922f6690679d86bdb6cdafb721e3a5ed6bb674ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917122"
---
# <a name="rowset-property-ado"></a>Rowset 属性 (ADO)
获取或设置**ADORecordsetConstruction**对象上/的 OLE DB**行集**对象。 使用 put_Rowset 时，行集会转换为 ADO**记录集**对象。  
  
 读/写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>参数  
 *ppRowset*  
 指向 OLE DB**行集**对象的指针。  
  
 *PRowset*  
 一个 OLE DB**行集**对象。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回标准的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>应用于  
 [ADORecordsetConstruction 接口](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
