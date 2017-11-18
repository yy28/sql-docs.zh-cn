---
title: "getURL 方法 (int) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getURL Ijnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 75d03ced-3614-4997-9abd-24642b1d1aae
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89feb3812a54d9c651d7fd36a07886d94782290d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="geturl-method-int"></a>getURL 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  与给定的参数索引的 Java 编程语言中某个 URL 对象中检索指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.net.URL getURL(int n)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 **Int** ，该值指示参数索引。  
  
## <a name="return-value"></a>返回值  
 一个 URL。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getURL 方法指定此 getURL 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getURL 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

