---
title: "setSavepoint 方法 (java.lang.String) |Microsoft 文档"
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
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5674fa6b4bff1518a4b693b06980e40a2da463b3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setsavepoint-method-javalangstring"></a>setSavepoint 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  具有给定名称在当前事务中，创建保存点并返回新[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)表示它的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sName*  
  
 A**字符串**值，该值包含的保存点的名称。  
  
## <a name="return-value"></a>返回值  
 一个保存点对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 setSavePoint 方法指定此 setSavePoint 方法。  
  
 *SName*自动转义参数[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [setSavepoint 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
