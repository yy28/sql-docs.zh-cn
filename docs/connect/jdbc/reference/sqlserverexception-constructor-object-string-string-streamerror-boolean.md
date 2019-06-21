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
manager: jroth
ms.openlocfilehash: 33b5d593cfc5ac4b46fdfe7dcf7a845f754d5f3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800915"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException 构造函数 (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新实例[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)类在给定**对象**即**字符串**对象，**字符串**对象、 **StreamError**对象，和一个**布尔**。

## <a name="syntax"></a>语法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parameters  
 obj   
  
 IO 缓冲区生成了异常。

 *errText*  
  
 包含错误文本的字符串。
  
 *sqlState*  
  
 一个包含 SQL 状态的枚举对象。
 
 streamError   
  
 StreamError 对象，其中包含有关错误的详细信息。
 
 bStack   
  
 一个布尔值，该值指示是否应生成堆栈跟踪。
  
## <a name="see-also"></a>另请参阅  
 [SQLServerException 构造函数](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成员](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 类](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
