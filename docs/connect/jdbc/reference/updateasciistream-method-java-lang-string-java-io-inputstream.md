---
title: updateAsciiStream 方法 (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a9fbb5f5c74a549a84e54980d585b7b5c30f61a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798932"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>updateAsciiStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 ASCII 流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
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
 此 updateAsciiStream 方法由 java.sql.ResultSet 接口中的 updateAsciiStream 方法指定。  
  
 此方法将 InputStream 对象中的 ASCII 字符（字节）传递给可转换的字符列，即 Unicode 的 ASCII 范围 [0x00 - 0x7F] 以及 874、932、936、949、950 和 1250-1258 代码页。 此方法执行到目标排序规则页的转换。 尝试更新不可转换的目标列将引发异常。 对于二进制列，会传递原始字节。  
  
 使用此方法对于**图像**，**文本**，并**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型可能会影响性能。  
  
## <a name="see-also"></a>另请参阅  
 [updateAsciiStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
