---
title: getSelectMethod 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.getSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6255d2e-0028-474a-afa8-553ef092243e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0364a431020ff73bc5590dbbfa12d20f401b9ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getselectmethod-method-sqlserverdatasource"></a>getSelectMethod 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用于使用此创建的所有结果集的默认游标类型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSelectMethod()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**包含默认游标类型的值。  
  
## <a name="remarks"></a>注释  
 selectMethod 属性指定用于结果集的默认游标类型。 处理大型结果集并不希望将整个结果设置在客户端上的内存中存储时，此属性很有用。 通过将属性设置为“cursor”，可以创建可一次提取更小数据块区的服务器端游标。 如果未设置 selectMethod 属性，getSelectMethod 将返回默认值“direct”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
