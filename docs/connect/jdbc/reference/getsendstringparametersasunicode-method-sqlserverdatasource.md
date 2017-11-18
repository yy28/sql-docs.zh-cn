---
title: "getSendStringParametersAsUnicode 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 520e40a43f47536b34ef68ebebde73f199c8e915
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>getSendStringParametersAsUnicode 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**布尔**值，该值指示是否启用发送到服务器以 UNICODE 格式的字符串参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果字符串参数发送到 UNICODE 格式中的服务器。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 sendStringParametersAsUnicode 属性设置为**true**默认值时，字符串参数发送到 UNICODE 格式中的服务器。 如果 sendStringParametersAsUnicode 设置为**false**，字符串参数发送到服务器 ASCII/MBCS 格式，而不是在 UNICODE。 如果未设置 sendStringParametersAsUnicode，getSendStringParametersAsUnicode 返回的默认值**true**。  
  
 有关 sendStringParametersAsUnicode 连接属性的详细信息，请参阅[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

