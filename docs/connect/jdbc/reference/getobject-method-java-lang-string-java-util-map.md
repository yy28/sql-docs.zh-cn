---
title: getObject 方法 (java.lang.String, java.util.Map) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String, Java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e174eb81-d569-479e-a171-365cd6d44b6a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8803ead9f5ec779a024a0f1980b0e3dab3a746ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981148"
---
# <a name="getobject-method-javalangstring-javautilmap"></a>getObject 方法 (java.lang.String, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  通过使用给定的 Map 对象，在给定参数名称的情况下检索指定参数的值作为 Java 编程语言中的对象。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支持此方法。 如果使用此方法，则将始终返回默认映射。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol,  
                                  java.util.Map m)  
```  
  
#### <a name="parameters"></a>Parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *m*  
  
 地图对象。  
  
## <a name="return-value"></a>返回值  
 Object 值  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getObject 方法是由 java.sql.CallableStatement 接口中的 getObject 方法指定的。  
  
 此方法将返回给定列的值作为一个 Java 对象。 根据 JDBC 规范中指定的内置类型映射，Java 对象的类型将为对应于此列 SQL 类型的默认 Java 对象类型。 如果此值为 SQL NULL，则驱动程序会返回 Java null。  
  
 也可使用此方法来读取数据库特定的抽象数据类型。 在 JDBC 2.0 API 中，getObject 方法的行为已扩展为具体化 SQL 用户定义类型的数据。 当列包含结构化或非重复值时，此方法的行为则类似于对 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())` 进行调用。  
  
 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 开始：  
  
-   date 类型的值将作为 java.sql.Date 对象返回  。  
  
-   time 类型的值将作为 java.sql.Time 对象返回  。  
  
-   datetime2 类型的值将作为 java.sql.Timestamp 对象返回  。  
  
-   datetimeoffset 类型的值将作为 microsoft.sql.DateTimeOffset 对象返回  。  
  
## <a name="see-also"></a>另请参阅  
 [getObject 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
