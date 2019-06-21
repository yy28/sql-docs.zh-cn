---
title: getClob 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getClob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91020fad-a9e2-4ea4-9c72-c63cf6b1051c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e5650d900cd4cf4bcbb8a33501ad49c3f1a8607c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66763785"
---
# <a name="getclob-method-int-sqlserverresultset"></a>getClob 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Java 编程语言中的 Clob 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Clob getClob(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 Clob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getClob 方法是由 java.sql.ResultSet 接口中的 getClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
