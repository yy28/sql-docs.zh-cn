---
title: setSendTimeAsDatetime 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ded6641232939ce0f76ade9f332646bbdd4c4d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927826"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此方法。  
  
 修改 sendTimeAsDatetime  连接属性的设置。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>parameters  
 *sendTimeAsDateTime*  
  
 一个布尔值。 如果设置为 true，java.sql.Time 值将作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 类型发送到服务器  。 如果设置为 false，java.sql.Time 值将作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] time 类型发送到服务器  。  
  
## <a name="remarks"></a>备注  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) 返回“sendTimeAsDatetime”连接属性的设置  。  
  
 有关 sendTimeAsDatetime  连接属性的详细信息，请参阅[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 有关详细信息，请参阅[配置将 java.sql.Time 值发送到服务器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
