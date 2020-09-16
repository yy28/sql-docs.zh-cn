---
description: setString 方法 (SQLServerCallableStatement)
title: setString 方法 (SQLServerCallableStatement) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ab66f76ccc0f6c80c9358e56902c063ca5e1e15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450709"
---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 Java String **** 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>参数  
 sCol**  
  
 一个字符串，该字符串包含参数的名称****。  
  
 *s*  
  
 一个字符串值****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setString 方法是由 java.sql.CallableStatement 接口中的 setString 方法指定的。  
  
 仅在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 知道目标类型为二进制时，才会执行字符串到二进制的转换。 如果 JDBC 驱动程序不知道基础类型，它将会传递 String 文本并在服务器不能执行转换时返回一个服务器错误****。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
