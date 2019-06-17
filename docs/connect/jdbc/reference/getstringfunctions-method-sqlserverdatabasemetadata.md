---
title: getStringFunctions 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getStringFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb489ee-185e-405a-a4f7-3eb73c29bcd6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 20dfb1ecadbd417a79e74171e4f247e6b09ed40f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788709"
---
# <a name="getstringfunctions-method-sqlserverdatabasemetadata"></a>getStringFunctions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于此数据库的 String  函数以逗号分隔的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getStringFunctions()  
```  
  
## <a name="return-value"></a>返回值  
 一个**字符串**，其中包含**字符串**函数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getStringFunctions 方法由 java.sql.DatabaseMetaData 接口中的 getStringFunctions 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
