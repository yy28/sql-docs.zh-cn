---
description: setString 方法 (long, java.lang.String) (SQLServerNClob)
title: setString 方法 (long, java.lang.String) - NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 944277e0bf3b8a701ceb9700f4b70a71cdec8d25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450736"
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>setString 方法 (long, java.lang.String) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的 String**** 写入起始于指定位置的 NCLOB****。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>参数  
 pos  
  
 写入 NCLOB**** 的起始位置；第一个位置为 1。  
  
 *str*  
  
 要写入 NCLOB**** 的 String。  
  
## <a name="return-value"></a>返回值  
 写入的字符数。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setString 方法是由 java.sql.NClob 接口中的 setString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
