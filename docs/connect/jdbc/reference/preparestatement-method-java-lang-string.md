---
title: prepareStatement 方法 (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 72b5c4a5-1382-4b2c-80a0-47c97c5f52d3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 11ff6a1b5c919f44bfc9cfd56e1e94ac57b673e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802651"
---
# <a name="preparestatement-method-javalangstring-int"></a>prepareStatement 方法 (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象，此对象用于将参数化 SQL 语句发送到数据库，并能返回给定数组所指定的自动生成键。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
 columnIndexes   
  
 整数的数组。  
  
## <a name="return-value"></a>返回值  
 一个 PreparedStatement 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 prepareStatement 方法由 java.sql.Connection 接口中的 prepareStatement 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [prepareStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
