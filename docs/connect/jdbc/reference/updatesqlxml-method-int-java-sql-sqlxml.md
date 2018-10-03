---
title: updateSQLXML 方法 （int，java.sql.SQLXML） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 451e4bbd85e5e3743ac137da3b4a2257e6a8c53c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643856"
---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>updateSQLXML 方法 (int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.SQLXML 值更新指定列  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
 *xmlObject*  
  
 SQLXML 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateSQLXML 方法由 java.sql.ResultSet 接口中的 updateSQLXML 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateSQLXML Method (SQLServerResultSet)](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
