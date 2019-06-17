---
title: getShort 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getShort (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cd9773c1-b598-4adb-aaf6-0c0f589cbef5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e09eafa55aae940a435522054df051cd84c4e4a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791812"
---
# <a name="getshort-method-int"></a>getShort 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定参数索引的情况下，检索指定参数的值作为 Java 编程语言中的 short  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public short getShort(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个**短**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getShort 方法是由 java.sql.CallableStatement 接口中的 getShort 方法指定的。  
  
 只有可以安全返回整数值的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型（例如 smallint、tinyint 和 bit）才支持此方法    。 在任何其他数据类型上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getShort 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
