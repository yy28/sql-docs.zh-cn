---
title: updateNClob 方法 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 87621ca7-e64a-49e2-b9c2-551390adaa26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 429ff64469bb904a3cc8de65f518b0e5fa72abad
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67998614"
---
# <a name="updatenclob-method-javalangstring-javaioreader"></a>updateNClob 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 Readerobject 更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>parameters  
 columnLabel   
  
 指示列标签的字符串  。  
  
 reader   
  
 Reader 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateNClob 方法是由 java.sql.ResultSet 接口中的 updateNClob 方法指定的。  
  
 只有 nvarchar(max)  、ntext  和 xml  列支持此方法。 在任何其他数据类型上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [updateNClob 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
