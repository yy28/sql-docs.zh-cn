---
description: updateNCharacterStream 方法 (java.lang.String, java.io.Reader)
title: updateNCharacterStream 方法 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 504d7d06-0227-45e1-8b01-899c3e6006e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a7df65888a1f56173f1820f0528bdd323a463c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353293"
---
# <a name="updatencharacterstream-method-javalangstring-javaioreader"></a>updateNCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>参数  
 columnLabel**  
  
 一个包含列标签的字符串。  
  
 reader  
  
 Reader 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateNCharacterStream 方法是由 java.sql.ResultSet 接口中的 updateNCharacterStream 方法指定的。  
  
 此方法将来自 Reader 对象的 Unicode 字符传递给所选的 nchar、nvarchar(max)、ntext 和 xml 列。 在其他数据类型列上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [updateNCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
