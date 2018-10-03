---
title: getString 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 208fbad8a728775c8e8d985a6f7f28c7facc865f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773486"
---
# <a name="getstring-method-javalangstring"></a>getString 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定参数名称的情况下，检索指定参数的值作为 Java 编程语言中的字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
## <a name="return-value"></a>返回值  
 一个字符串值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getString方法是由 java.sql.CallableStatement 接口中的 getString 方法指定的。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的所有列都可作为字符串返回。 这意味着可以返回基于数字和基于字符的所有类型的字符串表示形式，以及二进制列（如 binary、varbinary、varbinary(max)、image、timestamp 和 uniqueidentifier）的十六进制字符串表示形式。  
  
 位置敏感类型（例如 money、smallmoney, datetime、smalldatetime、float、real、decimal 和 numeric）将返回基础类型值的规范 toString() 格式。  
  
 用户定义类型将作为十六进制字符串值返回。  
  
## <a name="see-also"></a>另请参阅  
 [getString 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
