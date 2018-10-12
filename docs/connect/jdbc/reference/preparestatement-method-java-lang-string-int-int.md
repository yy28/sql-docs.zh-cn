---
title: prepareStatement 方法 (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5bb96dbe-f673-41b5-911b-8f661cca071a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95c3f823e230a51ada0f966c68a71b189eb482d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812385"
---
# <a name="preparestatement-method-javalangstring-int-int"></a>prepareStatement 方法 (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象，该对象使用给定的类型和并发机制生成 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sSql,  
                                                   int resultSetType,  
                                                   int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sSql*  
  
 包含 SQL 语句的 String。  
  
 *resultSetType*  
  
 指示结果集类型的 int。  
  
 *resultSetConcurrency*  
  
 指示结果集并发类型的 int。  
  
## <a name="return-value"></a>返回值  
 一个 PreparedStatement 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 prepareStatement 方法由 java.sql.Connection 接口中的 prepareStatement 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 方法](../../../connect/jdbc/reference/sqlserverconnection-methods.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
