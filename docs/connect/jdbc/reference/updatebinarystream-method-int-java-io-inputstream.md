---
description: updateBinaryStream 方法 (int, java.io.InputStream)
title: updateBinaryStream 方法 (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0920ccd4b4e22de19c03feb8ccee9735d00d2109
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354093"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>updateBinaryStream 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用二进制流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 *x*  
  
 InputStream 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateBinaryStream 方法是由 java.sql.ResultSet 接口中的 updateBinaryStream 方法指定的。  
  
 将此方法应用于 image****、text**** 和 ntext****[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型可能会影响性能。  
  
 此方法将来自 InputStream 对象的字节传递给所选的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二进制列，例如 binary、varbinary、varbinary(max)、image、xml 和 udt。 此方法不支持更新字符列。 若要使用 InputStream 更新字符列，请使用 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateBinaryStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
