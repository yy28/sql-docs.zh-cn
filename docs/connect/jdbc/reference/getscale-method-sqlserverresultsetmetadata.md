---
title: getScale 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fe29aa5f-4cc5-413f-8bbd-a58064993d87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c43d503fafba7d6dad8f7d982ad2f51542c61c4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980187"
---
# <a name="getscale-method-sqlserverresultsetmetadata"></a>getScale 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取指定列的小数点右侧的位数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getScale(int column)  
```  
  
#### <a name="parameters"></a>parameters  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个 int 值，此值指示列的小数位数  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getScale 方法由 java.sql.ResultSetMetaData 接口中的 getScale 方法指定的。  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 在 DECIMAL_DIGITS 列中的行为发生了更改。 有关详细信息，请参阅 [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
