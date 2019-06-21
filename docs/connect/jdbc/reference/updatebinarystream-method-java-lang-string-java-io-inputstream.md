---
title: updateBinaryStream 方法 (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3557c60f36ea48a8cb03f58997bc2d8093f432e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787312"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>updateBinaryStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用二进制流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnLabel   
  
 一个包含列标签的字符串  。  
  
 *x*  
  
 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBinaryStream 方法由 java.sql.ResultSet 接口中的 updateBinaryStream 方法指定。  
  
 使用此方法对于**图像**，**文本**，并**ntext** SQL Server 数据类型可能会影响性能。  
  
 此方法将来自 InputStream 对象的字节传递给所选的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二进制列，例如 binary、varbinary、varbinary(max)、image、xml 和 udt。 此方法不支持更新字符列。 若要使用 InputStream 更新字符列，请使用 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateBinaryStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
