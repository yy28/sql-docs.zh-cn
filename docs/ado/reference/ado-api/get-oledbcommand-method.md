---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d32d79b0a0481d2ade05a78c80d72587817a04b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918574"
---
# <a name="getoledbcommand-method"></a>get_OLEDBCommand 方法
返回基础 OLE DB 命令，首先传播到 OLE DB 命令 ADO 命令上设置的任何参数信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 *ppOLEDBCommand*  
 [out]指向在其中写入基础 OLE DB 命令的 IUnknown 指针的指针位置的指针。  
  
## <a name="applies-to"></a>适用范围  
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
