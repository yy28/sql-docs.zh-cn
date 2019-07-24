---
title: updateObject 方法 (java.lang.String, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6999d9c-eab6-4e4d-96d8-e0fa4b4b87e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de499e4cc11f1da1780878e4c921d161ee8b2693
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998444"
---
# <a name="updateobject-method-javalangstring-javalangobject"></a>updateObject 方法 (java.lang.String, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用 Object 值更新指定的列  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 obj   
  
 Object 值  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateObject 方法是由 java.sql.ResultSet 接口中的 updateObject 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateObject 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
