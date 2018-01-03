---
title: "put_OLEDBCommand 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3584728624fb01d49a693bfbb2d09a655311d55b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="putoledbcommand-method"></a>put_OLEDBCommand 方法
此方法不执行任何操作并始终返回，则为 S_OK。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 *pOLEDBCommand*  
 [in]指向 OLE DB 命令对象的指针。  
  
## <a name="applies-to"></a>适用范围  
 [IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)
