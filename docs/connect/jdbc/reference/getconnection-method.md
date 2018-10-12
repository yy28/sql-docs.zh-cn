---
title: getConnection 方法 （) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f520e96-5313-468f-b987-535ddaea027e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0c41bee354b916c1a52f71edfce925012e1a301
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759045"
---
# <a name="getconnection-method-"></a>getConnection 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  尝试与此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象表示的数据源建立连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>返回值  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 getConnection 方法由 javax.sql.DataSource 接口中的 getConnection 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [getConnection 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
