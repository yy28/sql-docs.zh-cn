---
title: getDateTimeOffset(java.lang.string) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e585927c-0dee-43fd-b71e-c9f1701790bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a929b5869e58f4f1207b14474302fdb247251850
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983863"
---
# <a name="getdatetimeoffsetjavalangstring-sqlserverresultset"></a>getDateTimeOffset(java.lang.string) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此方法。  
  
 在给定参数索引的情况下，检索指定列的值作为 Java 编程语言中的 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 列的名称。  
  
## <a name="return-value"></a>返回值  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 可以使用[SQLServerResultSet](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)更新[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)的值。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
