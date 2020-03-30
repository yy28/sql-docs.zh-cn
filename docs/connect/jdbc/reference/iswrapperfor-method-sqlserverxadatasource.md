---
title: isWrapperFor 方法 (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e32cbf975d156aae723dfbff105fe51e039dc1b5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977022"
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>isWrapperFor 方法 (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示此对象是否为指定接口的包装。  
  
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
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) 方法和 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) 方法由在 JDBC 4.0 规范中引入的 java.sql.Wrapper 接口定义。  
  
 如果此方法返回 true，则将使用同一参数成功调用 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)。  
  
 有关详细信息，请参阅[包装器和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另请参阅  
 [unwrap 方法 (SQLServerXADataSource)](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成员](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 类](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
