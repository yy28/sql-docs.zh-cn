---
title: getTimestamp 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a9fd6496-c72e-4cc6-b46a-4aa9f13f90ff
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2d9789e3c7fd8828fef3369ce08a8af7329e8c16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776805"
---
# <a name="gettimestamp-method-int"></a>getTimestamp 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，检索指定参数的值作为 Java 编程语言中的 java.sql.Timestamp 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Timestamp getTimestamp(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTimestamp 方法是由 java.sql.CallableStatement 接口中的 getTimestamp 方法指定的。  
  
 此方法只从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 和 smalldatetime 列返回值   。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
