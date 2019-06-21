---
title: updateDate 方法 (java.lang.String, java.sql.Date) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDate (java.lang.String, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fbe9123-7365-4a8f-bbd5-dc2b16f1b231
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b1ba26a22d3ee06041b6a6db051ad6363fa393b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66804244"
---
# <a name="updatedate-method-javalangstring-javasqldate"></a>updateDate 方法 (java.lang.String, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用日期值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateDate(java.lang.String columnName,  
                       java.sql.Date x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 日期值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateDate 方法是由 java.sql.ResultSet 接口中的 updateDate 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateDate 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
