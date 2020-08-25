---
description: get_OLEDBCommand 方法
title: get_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 56148afcd3c7d3e18e856c6e50a44f35aaa1bc64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775126"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand 方法
返回基础 OLE DB 命令，首先将在 ADO 命令上设置的所有参数信息传播到 OLE DB 命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>parameters  
 *ppOLEDBCommand*  
 弄一个指针，指向将写入基础 OLE DB 命令的 IUnknown 指针的指针位置。  
  
## <a name="applies-to"></a>适用于  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))