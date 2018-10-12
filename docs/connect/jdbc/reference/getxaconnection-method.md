---
title: getXAConnection 方法 （) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2710613-78b1-438f-b996-c7ae6f34381a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7cffeb3479174f5bc79eff52331f5a9d0e46e65
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687675"
---
# <a name="getxaconnection-method-"></a>getXAConnection 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  尝试建立可在分布式事务中使用的物理数据库连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.sql.XAConnection getXAConnection()  
```  
  
## <a name="return-value"></a>返回值  
 XAConnection 对象。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 getXAConnection 方法由 javax.sql.XADataSource 接口中的 getXAConnection 方法指定。  
  
> [!NOTE]  
>  此方法一般由 XA 连接池实现调用，而不由常规的 JDBC 应用程序代码调用。  
  
## <a name="see-also"></a>另请参阅  
 [getXAConnection 方法 &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成员](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 类](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
