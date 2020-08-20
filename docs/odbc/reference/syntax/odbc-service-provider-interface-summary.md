---
description: ODBC 服务提供程序接口摘要
title: ODBC 服务提供程序接口摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00d15d33fba1e697eebbe6a640c4f8a4d8eadea7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487340"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服务提供程序接口摘要
下表介绍了 ODBC 服务提供程序接口函数。 有关每个函数的语法和语义的详细信息，请参阅 [ODBC 服务提供程序接口 (SPI) Reference](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函数名称|用途|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|与 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同，但它在连接信息标记而不是连接句柄上设置属性。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|将连接字符串设置为应用程序的 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 调用的连接信息令牌。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|将数据源、用户 ID 和密码设置为应用程序的 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 调用的连接信息令牌。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|检索池 ID。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|确定驱动程序是否可以重复使用连接池中的现有连接。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果池中不能重复使用连接，则创建一个新连接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知驱动程序池 ID 已超时。|
