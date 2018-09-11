---
title: setMaxRows 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 292eb65a07cea177804bb2685147b05dd4cc961e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784688"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将任何 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象可包含的最大行数限制设置为给定的数目。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parameters  
 max  
  
 一个 int 值，此值指示最大行数；如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setMaxRows 方法由 java.sql.Statement 接口中的 setMaxRows 方法指定。  
  
 此 setMaxRows 方法对动态可滚动的游标并无影响。 应用程序应使用 SELECT TOP N SQL 语法来限制从可能较大的结果集中返回的行数。  
  
 当调用 setMaxRows 方法时，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 会在运行应用程序的查询时执行 SET ROWCOUNT SQL 语句。 这将导致 JDBC 驱动程序会限制受到由该查询执行的所有 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句所影响的行的最大数量，而不仅仅是该查询所返回的行数。 如果应用程序需要设置仅针对顶级 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的限制，则应在查询中使用 SELECT TOP N SQL 语法，而非 setMaxRows 方法。  
  
 有关 SET ROWCOUNT SQL 语句的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“[SET ROWCOUNT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)”主题。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
