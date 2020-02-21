---
title: SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1cc42a09e455fa42d3f89b05903a22afc945424
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67971121"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  当 object  、string  对象、string  对象、StreamError  对象和 boolean  给定时，初始化 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 类的新实例。

## <a name="syntax"></a>语法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>parameters  
 obj   
  
 生成了异常的 IO 缓冲区。

 *errText*  
  
 包含错误文本的字符串。
  
 *sqlState*  
  
 包含 SQL 状态的枚举对象。
 
 streamError   
  
 包含错误详细信息的 StreamError 对象。
 
 bStack   
  
 指明是否应生成堆栈跟踪的 boolean。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
