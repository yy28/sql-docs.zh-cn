---
title: "setMaxRows 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b08d78a404c0454600072d9b227761d8c27045cc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  对任何设置的最大行数限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象可以包含到指定的数字。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parameters  
 *最大值*  
  
 **Int** ，该值指示最大行数或 0，如果没有任何限制。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 setMaxRows 方法指定此 setMaxRows 方法。  
  
 此 setMaxRows 方法不起为动态的可滚动游标。 应用程序应使用 SELECT TOP N SQL 语法来限制从可能较大的结果集中返回的行数。  
  
 当调用 setMaxRows 方法时，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]运行应用程序的查询时执行的设置 ROWCOUNT SQL 语句。 这将导致要限制的最大的所有受影响的行数的 JDBC 驱动程序[!INCLUDE[tsql](../../../includes/tsql_md.md)]执行该查询，而不仅仅是行数返回由该查询的语句。 如果应用程序需要以仅在顶级上设置的限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象时，它应在查询中而不是 setMaxRows 方法使用选择的 TOP N SQL 语法。  
  
 有关设置 ROWCOUNT SQL 语句的详细信息，请参阅"[SET ROWCOUNT (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)"中的主题[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
