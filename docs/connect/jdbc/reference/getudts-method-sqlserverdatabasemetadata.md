---
title: getUDTs 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e90f4d2ea8b98d2ecef237f04f5fe290a512c92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765902"
---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>getUDTs 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索特定架构中定义的由用户定义的类型的说明。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支持此方法。 如果使用此方法，则将始终返回一个空结果集。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
 schemaPattern   
  
 一个包含架构名称模式的字符串  。  
  
 typeNamePattern   
  
 一个包含类型名称模式的 String  。  
  
 *types*  
  
 含有要包含的数据类型的整数数组。 Null 指示应包含所有类型。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getUDTs 方法是由 java.sql.DatabaseMetaData 接口中的 getUDTs 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
