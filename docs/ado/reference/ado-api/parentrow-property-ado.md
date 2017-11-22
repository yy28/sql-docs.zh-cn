---
title: "ParentRow 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords: ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8869e091c0f48981d60893ed0d3f698aeee0c8b2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="parentrow-property-ado"></a>ParentRow 属性 (ADO)
设置 OLE DB 的容器**行**对象上**ADORecordConstruction**对象，以便父行转换为 ADO**记录**对象。  
  
 只写。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parameters  
 *pParent*  
 行的容器。  
  
## <a name="return-values"></a>返回值  
 此属性方法返回的标准的 HRESULT 值，包括，则为 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>适用范围  
 [ADORecordConstruction 接口](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
