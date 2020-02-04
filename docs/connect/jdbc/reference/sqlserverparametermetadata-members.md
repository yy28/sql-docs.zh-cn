---
title: SQLServerParameterMetaData 成员 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 82e005a4e81dd08643613f0c90dafbd9124dd3bb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970876"
---
# <a name="sqlserverparametermetadata-members"></a>SQLServerParameterMetaData 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过 [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 类公开的成员。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
  
|名称|说明|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn、parameterModeInOut、parameterModeOut、parameterModeUnknown、parameterNoNulls、parameterNullable、parameterNullableUnknown|  
  
## <a name="methods"></a>方法  
  
|名称|说明|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|检索指定 Java 类的完全限定名称，而该 Java 类的实例应传递给 [SQLServerPreparedStatement](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 类中的 [setObject](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 方法。|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|检索指定 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象中的参数数目，此 [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 对象包含该指定对象的信息。|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|检索指定参数的模式。|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|检索指定参数的 SQL 类型。|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|检索指定参数的数据库特定类型名称。|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|检索指定参数的小数位数。|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|检索指定参数的小数点右侧的位数。|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|检索指定参数中是否允许 Null 值。|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|检索指定参数的值能否为带正负号的数字。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
