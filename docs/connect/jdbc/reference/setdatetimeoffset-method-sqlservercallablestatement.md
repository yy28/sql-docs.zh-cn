---
title: "setDateTimeOffset 方法 (SQLServerCallableStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9383e14d-c83e-43c5-980c-50a3e0bedc31
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb801d286db8f1f9a861508b15d0b50294c10419
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setdatetimeoffset-method-sqlservercallablestatement"></a>setDateTimeOffset 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  此方法已添加到中[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0。  
  
 设置为指定的列的值[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setDateTimeOffset(String sCol, microsoft.sql.DateTimeOffset t)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 列的名称。  
  
 *t*  
  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 你可以检索[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)值与[SQLServerCallableStatement.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)。  
  
 [setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)采用的列序号。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

