---
title: 解包方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81e533e32504df219155259e9639c83c3be4c647
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985600"
---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>unwrap 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个实现指定接口的对象，从而允许访问特定于 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parameters  
 iface   
  
 定义接口的类型为 T 的类  。  
  
## <a name="return-value"></a>返回值  
 实现指定接口的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)方法由在 JDBC 4.0 规范中引入的 java.sql.Wrapper 接口定义。  
  
 应用程序可能需要访问特定于 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的 JDBC API 扩展。 如果类公开供应商扩展，则 unwrap 方法支持对此对象扩展的公共类取消包装。  
  
 调用此方法时，对象会取消对下列类的包装：[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 和 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。  
  
 有关代码示例, 请参阅[解&#40;包&#41;方法 SQLServerCallableStatement](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)。  
  
 有关详细信息, 请参阅[包装器和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [isWrapperFor 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
