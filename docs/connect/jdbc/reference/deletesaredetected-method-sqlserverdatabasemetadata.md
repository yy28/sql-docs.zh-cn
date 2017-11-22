---
title: "deletesAreDetected 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.deletesAreDetected
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2556d8866102f2921c1e17a07f67687a710edf26
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>deletesAreDetected 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  可以通过调用检测是否可见的行删除的检索[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean deletesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>Parameters  
 *type*  
  
 **Int** ，该值指示结果集类型，如 java.sql.ResultSet 或 SQLServerResultSet 中定义可以是以下值之一：  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet 类型  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet 类型  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>返回值  
 **true**如果一个口取代删除的行。 **false**如果删除已删除的行。  
  
 使用时[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，此方法返回**true**为 TYPE_SS_SCROLL_KEYSET 游标和**false**对于所有其他结果集类型。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 deletesAreDetected 方法指定此 deletesAreDetected 方法。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]尽管检测，则为正向和动态游标的暂时性检测对于所有可更新的游标类型，已删除的行。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
