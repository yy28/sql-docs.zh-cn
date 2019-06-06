---
title: DataSpace (ADO-WFC 语法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52e58cb358a28169a11b16e2c4d9f64ba4745bad
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695473"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace（ADO - WFC 语法）
**CreateObject**方法**DataSpace**类指定这两个业务对象来处理客户端应用程序请求 (*progid*) 和通信协议和服务器 (*连接*)。 **createObject**将返回[ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md)表示服务器的对象。  
  
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
### <a name="constructor"></a>构造函数  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>方法  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>属性  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>请参阅  
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
