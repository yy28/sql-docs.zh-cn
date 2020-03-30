---
title: prepareCall 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb83b567-4ce5-447a-93cc-895d4eaf3a05
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dd0a5c40cf12ddae0c6a7aae00c6a83bfe6549f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976218"
---
# <a name="preparecall-method-javalangstring"></a>prepareCall 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建用于调用数据库存储过程的 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
## <a name="return-value"></a>返回值  
 CallableStatement 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 prepareCall 方法是由 java.sql.Connection 接口中的 prepareCall 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [prepareCall 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
