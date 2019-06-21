---
title: setString 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: abbb07c23685562d28297f096728589fdc3a343e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66773498"
---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 Java String  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 一个字符串，该字符串包含参数的名称  。  
  
 *s*  
  
 一个字符串值  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setString 方法是由 java.sql.CallableStatement 接口中的 setString 方法指定的。  
  
 仅在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 知道目标类型为二进制时，才会执行字符串到二进制的转换。 如果 JDBC 驱动程序不知道基础类型，它将会传递 String 文本并在服务器不能执行转换时返回一个服务器错误  。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
