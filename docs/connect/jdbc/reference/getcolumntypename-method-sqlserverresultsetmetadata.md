---
title: getColumnTypeName 方法 (SQLServerResultSetMetaData) |Microsoft Docs
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
- SQLServerResultSetMetaData.getColumnTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a444da82-c1af-40a5-9774-02476416c92c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7955ad0d658af50f972f8bd76c5b96a2a78be18
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785581"
---
# <a name="getcolumntypename-method-sqlserverresultsetmetadata"></a>getColumnTypeName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定列的数据库特定的类型名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getColumnTypeName(int column)  
```  
  
#### <a name="parameters"></a>Parameters  
 *column*  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个包含列的服务器名称的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getColumnTypeName 方法由 java.sql.ResultSetMetaData 接口中的 getColumnTypeName 方法指定。  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 在 TYPE_NAME 列中的行为发生了更改。 有关详细信息，请参阅 [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
