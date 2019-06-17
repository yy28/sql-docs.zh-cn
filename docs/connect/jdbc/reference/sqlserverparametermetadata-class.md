---
title: SQLServerParameterMetaData 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1393d7c6a5665730517d8aa1f248eaadb0db65aa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773555"
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
  
## <a name="remarks"></a>Remarks  
 若要检索参数元数据，请使用 SET FMT ONLY 运行准备好的语句。 可调用的语句调用 sp_sproc_columns 来为过程参数检索名称和元数据。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
