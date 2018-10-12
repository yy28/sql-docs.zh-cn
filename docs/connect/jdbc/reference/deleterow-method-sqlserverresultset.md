---
title: deleteRow 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: 466fa86609ba4f784e78ba9ac0fb5178d827645e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784115"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  从此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象和基础数据库中删除当前行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 deleteRow 方法由 java.sql.ResultSet 接口中的 deleteRow 方法指定。  
  
 游标位于插入行时，无法调用此方法。  
  
 使用键集游标时，此方法在结果集中留有一个孔。 可以通过使用 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 方法测试此孔。 结果集中的行的行号不变。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
