---
title: getFunctions 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7bf039e2104a7ac2fbbcce8a5a9fbd8bade8589d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836022"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索系统函数和用户函数的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 数据库中的目录名称。 如果该名称为空字符串 ""，则结果将包括无目录的函数。 如果它是**null**，目录名称不用于搜索。  
  
 *schemaPattern*  
  
 架构的名称。 如果该名称为空字符串 ""，则结果将包括无架构的函数。 如果它是**null**，架构名称不用于搜索。  
  
 *functionNamePattern*  
  
 函数的名称。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getFunctions 方法指定此 getFunctions 方法。  
  
 此方法只返回与指定架构和函数名称匹配的系统函数和用户函数。  
  
> [!IMPORTANT]  
>  返回的结果集可包含调用用户无权执行的函数。  
  
 每个函数说明都包括以下列：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**字符串**|函数所在的数据库的名称。|  
|FUNCTION_SCHEM|**字符串**|函数所在的架构的名称。|  
|FUNCTION_NAME|**字符串**|函数的名称。|  
|NUM_INPUT_PARAMS|**int**|保留以供将来使用，当前返回 -1 值。|  
|NUM_OUTPUT_PARAMS|**int**|保留以供将来使用，当前返回 -1 值。|  
|NUM_RESULT_SETS|**int**|保留以供将来使用，当前返回 -1 值。|  
|REMARKS|**字符串**|有关函数的注释。|  
|FUNCTION_TYPE|**short**|函数的类型。 它可以是以下值之一：<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 返回的结果集中的所有说明都按 FUNCTION_CAT、FUNCTION_SCHEM、FUNCTION_NAME 和 SPECIFIC_NAME 排序。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
