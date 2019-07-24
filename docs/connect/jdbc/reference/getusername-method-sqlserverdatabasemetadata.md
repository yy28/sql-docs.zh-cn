---
title: getUserName 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUserName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1ae81034-5de3-4f4a-b3f2-7d9d198a73af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38da8d6666337c464d7a828952b025977336d373
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978138"
---
# <a name="getusername-method-sqlserverdatabasemetadata"></a>getUserName 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库可识别的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getUserName()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含用户名的字符串  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getUserName 方法是由 java.sql.DatabaseMetaData 接口中的 getUserName 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
