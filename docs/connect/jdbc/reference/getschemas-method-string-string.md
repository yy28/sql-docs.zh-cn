---
title: "getSchemas 方法 （String，String） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24176593bf253b1a5482ac5df74a558046148c96
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getschemas-method-string-string"></a>getSchemas 方法 (String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  通过使用指定目录名称和架构名称来检索当前数据库中可用的架构名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>Parameters  
 *目录*  
  
 数据库中的目录名称。 如果该名称为空字符串 ""，则结果将包括无目录的架构。 如果它是**null**，目录名称不用于搜索。  
  
 *schemaPattern*  
  
 架构的名称。 如果它是**null**，架构名称不用于搜索。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetSchemas 方法 java.sql.DatabaseMetaData 界面中指定此 getSchemas 方法。  
  
 GetSchemas 方法所返回的结果集包含以下信息：  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**字符串**|架构的名称。|  
|TABLE_CATALOG|**字符串**|架构的目录名称。|  
  
 通过 TABLE_CATALOG 然后 TABLE_SCHEM，对结果进行排序。 各行均以 TABLE_SCHEM 作为第一列并以 TABLE_CATALOG 作为第二列。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

