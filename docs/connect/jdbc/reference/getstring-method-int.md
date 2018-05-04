---
title: getString 方法 (int) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3fce8bf-8d6e-476f-aa6d-992daa79b899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc00f8c9057f0b4222603ccb281251d9b240aab8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getstring-method-int"></a>getString 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索与指定参数的值**字符串**java 编程语言提供的参数索引。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getString(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 **Int** ，该值指示参数索引。  
  
## <a name="return-value"></a>返回值  
 A**字符串**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetString 方法 java.sql.CallableStatement 界面中指定此 getString 方法。  
  
 中的所有列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以作为字符串返回。 这意味着可以返回基于数字和基于字符的所有类型的字符串表示形式，以及二进制列（如 binary、varbinary、varbinary(max)、image、timestamp 和 uniqueidentifier）的十六进制字符串表示形式。  
  
 如 money、 smallmoney、 datetime、 smalldatetime、 float、 real、 小数和数值的区分位置的类型将返回类型的基础值的规范的 tostring （） 格式。  
  
 用户定义类型将作为十六进制字符串值返回。  
  
## <a name="see-also"></a>另请参阅  
 [getString 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
