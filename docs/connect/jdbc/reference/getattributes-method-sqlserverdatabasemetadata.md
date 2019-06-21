---
title: getAttributes 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getAttributes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4dc784ed-4699-4197-9af5-6e03da80d14c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcd33cbb39286c03b5b809b847a8d8a2b8b609f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799963"
---
# <a name="getattributes-method-sqlserverdatabasemetadata"></a>getAttributes 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索给定架构和目录中可用的用户定义类型的给定类型的给定属性的说明。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支持此方法。 如果调用此方法，则将始终返回一个空结果集。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getAttributes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern,  
                                        java.lang.String attributeNamePattern)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
 schemaPattern   
  
 一个包含架构名称模式的字符串  。  
  
 typeNamePattern   
  
 一个包含类型名称模式的 String  。  
  
 attributePattern   
  
 一个包含属性名称模式的 String  。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getAttributes 方法由 java.sql.DatabaseMetaData 接口中的 getAttributes 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
