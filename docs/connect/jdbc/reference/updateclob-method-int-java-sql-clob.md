---
title: updateClob 方法 (int, java.sql.Clob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateClob (int, java.sql.Clob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2a5e9cb-2631-4f6e-a90c-4bee58e2f7b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb880b72e7ef6dc3a03beba28d3ae9b3ca7d3c44
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67999238"
---
# <a name="updateclob-method-int-javasqlclob"></a>updateClob 方法 (int, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定列索引时使用 java.sql.Clob 值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateClob(int columnIndex,  
                       java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 clobValue   
  
 Clob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateClob 方法是由 java.sql.ResultSet 接口中的 updateClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
