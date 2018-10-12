---
title: getFloat 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40178471-4f35-4df9-b3fb-80cdf43de274
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f40d9fc6fee6ade26f2279662175c5d91458d279
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829745"
---
# <a name="getfloat-method-int"></a>getFloat 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，检索指定参数作为 Java 编程语言中的 float 的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public float getFloat(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个**float**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getFloat 方法是由 java.sql.CallableStatement 接口中的 getFloat 方法指定的。  
  
 此方法使用 Java float 精度返回基于数字的所有类型。  
  
## <a name="see-also"></a>另请参阅  
 [getFloat 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
