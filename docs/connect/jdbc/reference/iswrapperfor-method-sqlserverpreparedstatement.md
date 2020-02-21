---
title: isWrapperFor 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b0e591b1-73e2-4f90-967f-5555eadfc3f1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ca21e48e1cd4d28337339a1aecc17b92bb259c2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977053"
---
# <a name="iswrapperfor-method-sqlserverpreparedstatement"></a>isWrapperFor 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此语句对象是否为指定接口的包装。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>parameters  
 iface   
  
 用于定义接口的 class  。  
  
## <a name="return-value"></a>返回值  
 如果此对象实现了接口或包装了实现接口的对象，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md) 方法和 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) 方法由在 JDBC 4.0 规范中引入的 java.sql.Wrapper 接口定义。  
  
 如果此方法返回 true，则将使用同一参数成功调用 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)。  
  
 有关详细信息，请参阅[包装器和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
