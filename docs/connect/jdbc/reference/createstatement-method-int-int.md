---
title: createStatement 方法 （int，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: df361da2387a053b9550c4b4e25dc94cced6579b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800639"
---
# <a name="createstatement-method-int-int"></a>createStatement 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象，该对象使用给定的类型和并发机制生成 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameters  
 resultSetType   
  
 表示结果集类型的 int  值。  
  
 resultSetConcurrency   
  
 **Int**值，该值表示结果集并发类型。  
  
## <a name="return-value"></a>返回值  
 将语句对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 createStatement 方法由 java.sql.Connection 接口中的 createStatement 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [createStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
