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
ms.openlocfilehash: 562b10fa67b04926e512833248c99ecb7b55a1fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443599"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand 方法
返回基础 OLE DB 命令，首先将在 ADO 命令上设置的所有参数信息传播到 OLE DB 命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>参数  
 *ppOLEDBCommand*  
 弄一个指针，指向将写入基础 OLE DB 命令的 IUnknown 指针的指针位置。  
  
## <a name="applies-to"></a>适用于  
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
