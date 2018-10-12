---
title: updateFloat 方法 （java.lang.String，float） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateFloat (java.lang.String, float)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19a6164f-f560-4304-8466-e55f0667a3d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 230585d601517c0809585be783b7f1afcbe56e8d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759385"
---
# <a name="updatefloat-method-javalangstring-float"></a>updateFloat 方法 (java.lang.String, float)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名使用 float 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateFloat(java.lang.String columnName,  
                        float x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
 *x*  
  
 一个**float**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateFloat 方法由 java.sql.ResultSet 接口中的 updateFloat 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateFloat 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
