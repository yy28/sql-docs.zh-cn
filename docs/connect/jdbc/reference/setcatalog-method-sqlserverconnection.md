---
title: setCatalog 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78b4d49029c6a0f2696cc93348bff7b32767bc13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974829"
---
# <a name="setcatalog-method-sqlserverconnection"></a>setCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将给定目录名称设置为选择在其中使用此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象的数据库的子空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setCatalog 方法由 setCatalog 方法在 sql 连接接口中指定。  
  
 *目录*参数由[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]自动转义。 使用此方法可为 Connection 对象设置目录属性。 无法通过任何其他方法隐式设置该属性。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
