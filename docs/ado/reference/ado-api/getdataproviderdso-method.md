---
description: GetDataProviderDSO 方法
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a45d78960b8b6b1ba2534e39f080a6c94fc0655
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443569"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 方法
从形状提供程序检索基础 OLE DB 数据源对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>参数  
 *ppDataProviderDSOIUnknown*  
 弄 指向指针的指针，该指针返回基础 OLE DB 数据源对象的 IUnknown。  
  
## <a name="remarks"></a>备注  
 此方法不会 addref 接口指针。 如果调用方计划持有指针，则调用方必须执行所需的 addref 和 release。  
  
## <a name="applies-to"></a>适用于  
 [IDSOShapeExtensions 接口](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
