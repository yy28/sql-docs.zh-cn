---
title: getTimestamp 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ad538a76-983f-4175-9481-9e7fa9480c71
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a404b80c855fa866f55114431dbb0e8fc2bb476e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778660"
---
# <a name="gettimestamp-method-int-sqlserverresultset"></a>getTimestamp 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引的值作为 Java 编程语言中的 java.sql.Timestamp 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Timestamp getTimestamp(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTimestamp 方法由 java.sql.ResultSet 接口中的 getTimestamp 方法指定。  
  
 此方法只从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 和 smalldatetime 列返回值。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
