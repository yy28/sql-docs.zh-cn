---
title: setServerName 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2a3c3c33fec8e36b799150dbe74dc69248e200d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920316"
---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置正在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的计算机的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>parameters  
 *serverName*  
  
 一个包含服务器名称的字符串  。  
  
## <a name="remarks"></a>备注  
 服务器名称为正在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的目标计算机的主机名。 如果未设置 serverName 属性，[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) 则将返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
