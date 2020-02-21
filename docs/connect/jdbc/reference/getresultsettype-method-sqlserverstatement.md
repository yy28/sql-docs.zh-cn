---
title: getResultSetType 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 260da35f-ddf6-4111-8519-69956ea3072e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a0293a48a354bba911a11ecf91a17211a9f8a12
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980298"
---
# <a name="getresultsettype-method-sqlserverstatement"></a>getResultSetType 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的结果集类型，这些对象由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getResultSetType()  
```  
  
## <a name="return-value"></a>返回值  
 指示结果集类型的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getResultSetType 方法是由 java.sql.Statement 接口中的 getResultSetType 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
