---
title: "SQLServerParameterMetaData 类 |Microsoft 文档"
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
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd97c5667d774829fb801ad22211d338afde1453
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverparametermetadata-class"></a>SQLServerParameterMetaData 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示用于预定义语句参数的元数据。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.lang.Object  
  
 **实现：** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>注释  
 若要检索参数元数据，请使用 SET FMT ONLY 运行准备好的语句。 可调用的语句调用 sp_sproc_columns 来为过程参数检索名称和元数据。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
