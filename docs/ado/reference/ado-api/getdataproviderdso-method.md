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
ms.openlocfilehash: e21e45d72cd5140c542fb6d6d0b150c414fb9832
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775066"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 方法
从形状提供程序检索基础 OLE DB 数据源对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>parameters  
 *ppDataProviderDSOIUnknown*  
 弄 指向指针的指针，该指针返回基础 OLE DB 数据源对象的 IUnknown。  
  
## <a name="remarks"></a>备注  
 此方法不会 addref 接口指针。 如果调用方计划持有指针，则调用方必须执行所需的 addref 和 release。  
  
## <a name="applies-to"></a>适用于  
 [IDSOShapeExtensions 接口](./idsoshapeextensions-interface.md)