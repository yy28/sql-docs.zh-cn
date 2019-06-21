---
title: getDate 方法 (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38ce7b75-2623-4eff-bc18-8cf7193adec8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c3106b0ada53fe2ccc096d789538dfea4cfc3e7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785709"
---
# <a name="getdate-method-int-javautilcalendar"></a>getDate 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在给定参数索引和 Calendar 对象的情况下，检索指定参数的值作为 Java 编程语言中的 java.sql.Date 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Date getDate(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示参数索引的 int  。  
  
 cal   
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 Date 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getDate 方法是由 java.sql.CallableStatement 接口中的 getDate 方法指定的。  
  
 此方法返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 数据类型的有效日期部分，时间部分设置为 Java 时间基线 00:00（午夜）   。  
  
## <a name="see-also"></a>另请参阅  
 [getDate 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
