---
title: DataSpace (ADO-WFC 语法) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160fe6068b86edc5d10f277dbd298954dc37838f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (ADO-WFC 语法)
**CreateObject**方法**DataSpace**类指定这两个业务对象用于处理客户端应用程序请求 (*progid*) 和通信协议和服务器 (*连接*)。 **createObject**返回[ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md)表示服务器的对象。  
  
## <a name="package-commswfcdata"></a>包 com.ms.wfc.data  
  
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
  
## <a name="see-also"></a>另请参阅  
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
