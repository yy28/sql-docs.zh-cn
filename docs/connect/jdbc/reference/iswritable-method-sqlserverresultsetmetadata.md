---
description: isWritable 方法 (SQLServerResultSetMetaData)
title: isWritable 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 50846aa8-e4e5-4fc3-a638-0e5fa8b597be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56f7d240f82209c46414e40d1c7b6518f198239e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433269"
---
# <a name="iswritable-method-sqlserverresultsetmetadata"></a>isWritable 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示是否能够成功在指定列上写入。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isWritable(int column)  
```  
  
#### <a name="parameters"></a>参数  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 如果对列成功执行写入操作，值为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isWritable 方法是由 java.sql.ResultSetMetaData 接口中的 isWritable 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
