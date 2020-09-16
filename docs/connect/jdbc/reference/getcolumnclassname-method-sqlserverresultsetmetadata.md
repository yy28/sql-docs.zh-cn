---
description: getColumnClassName 方法 (SQLServerResultSetMetaData)
title: getColumnClassName 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2c118790-5dd2-4b10-93b6-7f065ee324ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 143522437983b6e1d82ef8e617dbbb2ad7bd0222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436589"
---
# <a name="getcolumnclassname-method-sqlserverresultsetmetadata"></a>getColumnClassName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  如果调用 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) 方法来从列中检索值，则返回生成其实例的 Java 类的完全限定名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getColumnClassName(int column)  
```  
  
#### <a name="parameters"></a>参数  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 包含类的完全限定名称的 String****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getColumnClassName 方法是由 java.sql.ResultSetMetaData 接口中的 getColumnClassName 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
