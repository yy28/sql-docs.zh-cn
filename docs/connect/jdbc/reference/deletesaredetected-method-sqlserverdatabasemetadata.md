---
title: deletesAreDetected 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.deletesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6def9d94b1cbfb1b3e6bee07454d5f5adad2392
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785061"
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>deletesAreDetected 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索是否可通过调用 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 方法检测到可见行删除。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean deletesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>Parameters  
 *type*  
  
 指示结果集类型的 int，它可以为 java.sql.ResultSet 或 SQLServerResultSet 中定义的以下值之一：  
  
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
 **true**如果一个孔替代已删除的行。 **false**如果删除已删除的行。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库一起使用时，此方法将为 TYPE_SS_SCROLL_KEYSET 游标返回“true”，并且将为所有其他结果集类型返回“false”。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 deletesAreDetected 方法由 java.sql.DatabaseMetaData 接口中的 deletesAreDetected 方法指定。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将针对所有可更新的游标类型检测已删除的行，尽管此检测对于前进和动态游标是暂时的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
