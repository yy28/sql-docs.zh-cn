---
title: getArray 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getArray java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a98d159b-1fae-482a-9465-5411ce60f901
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05d5fb6bd412e55290ab893cf3552db6c6bcc34f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954347"
---
# <a name="getarray-method-javalangstring-sqlserverresultset"></a>getArray 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 Array 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Array getArray(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>parameters  
 *colName*  
  
 一个包含列名的字符串  。  
  
## <a name="return-value"></a>返回值  
 Array 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getArray 方法是由 java.sql.ResultSet 接口中的 getArray 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getArray 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
