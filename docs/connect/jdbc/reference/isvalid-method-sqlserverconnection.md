---
title: isValid 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 379d71b2100115bc1192a6f8f744b5afe92e5aed
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921089"
---
# <a name="isvalid-method-sqlserverconnection"></a>isValid 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象是否已关闭以及是否仍然有效。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>parameters  
 *timeout*  
  
 一个指定为验证连接而等待的秒数的整数  。  
  
## <a name="return-value"></a>返回值  
 如果连接有效，则为 true  ；如果连接无效或在超时之前无法确定连接是否有效，则为 false  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isValid 方法是由 java.sql.Connection 接口中的 isValid 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
