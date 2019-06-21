---
title: deleteRow 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987be5ee9fd49385acf02e52108e1e657fbc08a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786515"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow 方法 (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  从此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象和基础数据库中删除当前行。  
  
## <a name="syntax"></a>语法  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 deleteRow 方法由 java.sql.ResultSet 接口中的 deleteRow 方法指定。  
  
 游标位于插入行时，无法调用此方法。  
  
 使用键集游标时，此方法在结果集中留下间隙。 可以使用 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 方法来测试是否有此间隙。 结果集中的行的行号不变。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
