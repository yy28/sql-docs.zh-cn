---
title: setAsciiStream 方法 (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78eaf123b4d483a519c815f5063ce5f5af0caf21
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915813"
---
# <a name="setasciistream-method-sqlservernclob"></a>setAsciiStream 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索用于在指定起始位置将 ASCII 字符写入此 java.sql.NClob  对象表示的 NCLOB  值的流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>parameters  
 pos   
  
 写入 NCLOB  对象的起始位置；第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 表示可向其中写入 ASCII 编码字符的流的 OutputStream 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setAsciiStream 方法是由 java.sql.NClob 接口中的 setAsciiStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
