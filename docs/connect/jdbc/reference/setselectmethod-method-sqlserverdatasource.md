---
title: setSelectMethod 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7df9d7f066e9ddf076ba23b88c1d22b14d0f009d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925510"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于通过此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象创建的所有结果集的默认游标类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>parameters  
 *selectMethod*  
  
 一个包含默认游标类型的 String  值。  
  
## <a name="remarks"></a>备注  
 selectMethod 是用于结果集的默认游标类型。 当处理大型结果集且不想在客户端的内存中存储整个结果集时，此属性很有用。 通过将属性设置为“cursor”，可以创建可一次提取更小数据块区的服务器端游标。 如果未设置 selectMethod 属性，[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) 将返回默认值“direct”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
