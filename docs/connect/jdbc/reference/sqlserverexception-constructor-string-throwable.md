---
description: SQLServerException 构造函数 (java.lang.String, java.lang.Throwable)
title: SQLServerException 构造函数 (java.lang.String, java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd671bcb9c29eb7ac835c5bcbb877dc72c794c0a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450449"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangthrowable"></a>SQLServerException 构造函数 (java.lang.String, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定 string**** 对象和 throwable**** 对象时初始化 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 类的新实例。

## <a name="syntax"></a>语法  
  
```  
public SQLServerException(java.lang.String errText,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>参数  
 *errText*  
  
 包含错误文本的字符串。
 
 *cause*  
  
 一个 throwable 对象，该对象包含引发异常的原因。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
