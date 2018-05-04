---
title: ODBC 服务提供程序接口摘要 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29a19d20e6a69adf459ee1690e018bb7d237caf3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服务提供程序接口摘要
下表介绍 ODBC 服务提供程序接口函数。 有关语法和语义为每个函数的详细信息，请参阅[ODBC 服务提供程序接口 (SPI) 引用](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函数名称|用途|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|与相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，但它在连接信息令牌，而不是连接句柄上设置的属性。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|为应用程序的连接信息令牌设置的连接字符串[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)调用。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|为应用程序的连接信息令牌设置数据源、 用户 ID 和密码[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|检索池 id。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|确定驱动程序是否可以重用连接池中现有的连接。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果可以重复使用池中没有连接，请创建新的连接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知的驱动程序池 ID 已超时。|
