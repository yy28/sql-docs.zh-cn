---
title: createStatement 方法 （int，int） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7aaf58f311d4b3ebcd59cfd86aa07bc80ca1a2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="createstatement-method-int-int"></a>createStatement 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，它生成[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)与给定的类型和并发的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameters  
 *resultSetType*  
  
 **Int**表示的结果集类型的值。  
  
 *resultSetConcurrency*  
  
 **Int**值，该值表示结果集并发类型。  
  
## <a name="return-value"></a>返回值  
 语句对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 createStatement 方法指定此 createStatement 方法。  
  
## <a name="see-also"></a>另请参阅  
 [createStatement 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
