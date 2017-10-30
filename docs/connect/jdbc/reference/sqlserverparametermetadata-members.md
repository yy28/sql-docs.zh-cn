---
title: "SQLServerParameterMetaData 成员 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6fbc42820d6a35c054f705eefec36a9c05ee08c3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverparametermetadata-members"></a>SQLServerParameterMetaData 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
  
|Name|Description|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn、parameterModeInOut、parameterModeOut、parameterModeUnknown、parameterNoNulls、parameterNullable、parameterNullableUnknown|  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|检索其实例应传递给的 Java 类的完全限定名称[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)方法[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|检索中的参数数目[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)此对象[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)对象包含的信息。|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|检索指定参数的模式。|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|检索指定参数的 SQL 类型。|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|检索指定参数的特定于数据库的类型名称。|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|检索指定参数的小数位数。|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|检索指定参数的小数点右侧的位数。|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|检索指定参数中是否允许 Null 值。|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|检索指定参数的值能否为带正负号的数字。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

