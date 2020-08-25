---
description: put_OLEDBCommand 方法
title: put_OLEDBCommand 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: e386485f5e430a1bda50aa0d2059aeca90525af2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772766"
---
# <a name="put_oledbcommand-method"></a>put_OLEDBCommand 方法
此方法不执行任何操作，并且始终返回 S_OK。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>parameters  
 *pOLEDBCommand*  
 中指向 OLE DB Command 对象的指针。  
  
## <a name="applies-to"></a>适用于  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))