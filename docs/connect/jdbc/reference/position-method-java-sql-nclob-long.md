---
title: position 方法 (java.sql.NClob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea868190b635a9471bfad424d6fc74572970799b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976360"
---
# <a name="position-method-javasqlnclob-long"></a>position 方法 (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定的 NClob  对象 searchstr  在此 NClob  对象中出现的字符位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>parameters  
 searchstr   
  
 要搜索的 NClob 对象。  
  
 *start*  
  
 开始搜索的位置；第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 子字符串出现的位置，如果未出现，则为 -1。 第一个位置为 1。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 position 方法是由 ava.sql.NClob 接口中的 position 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [position 方法 (SQLServerNClob)](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
