---
title: GetDataProviderDSO 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2b5fbe59ab58b31cd0b796cbe46963683aa890b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932493"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 方法
从 Shape 提供程序检索基础 OLE DB 数据源对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 *ppDataProviderDSOIUnknown*  
 [out] 返回基础 OLE DB 数据源对象的 IUnknown 的指针指向的指针。  
  
## <a name="remarks"></a>备注  
 此方法执行不 addref 的接口指针。 如果调用方计划以容纳指针，调用方必须执行操作所需的 addref 和 release。  
  
## <a name="applies-to"></a>适用对象  
 [IDSOShapeExtensions 接口](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
