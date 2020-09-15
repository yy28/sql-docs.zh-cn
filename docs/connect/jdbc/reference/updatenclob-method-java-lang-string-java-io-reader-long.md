---
description: updateNClob 方法 (java.lang.String, java.io.Reader, long)
title: updateNClob 方法 (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ad5c8d9b-f8c8-4ddf-85c8-23420bba54ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6bd151c08cff98bba419d425d24ac0160ffc42d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431259"
---
# <a name="updatenclob-method-javalangstring-javaioreader-long"></a>updateNClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用具有指定字符数长度的指定 Reader**** 对象更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>参数  
 columnLabel**  
  
 指示列标签的字符串****。  
  
 reader  
  
 Reader 对象。  
  
 *length*  
  
 参数数据中的字符数。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateNClob 方法是由 java.sql.ResultSet 接口中的 updateNClob 方法指定的。  
  
 只有 nvarchar(max)****、ntext**** 和 xml**** 列支持此方法。 在任何其他数据类型上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [updateNClob 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
