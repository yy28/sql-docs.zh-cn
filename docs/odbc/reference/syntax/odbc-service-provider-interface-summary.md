---
title: ODBC 服务提供程序接口摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e351f08a5e72966c92a7452872532b90e4127964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837465"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服务提供程序接口摘要
下表介绍 ODBC 服务提供程序接口函数。 有关语法和语义为每个函数的详细信息，请参阅[ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函数名称|用途|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|与相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，但它的连接信息令牌而不是连接句柄上设置的属性。|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|为应用程序的连接信息令牌设置的连接字符串[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)调用。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|为应用程序的连接信息令牌设置数据源、 用户 ID 和密码[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|检索池 id。|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|确定是否驱动程序可以重复使用现有连接池中的连接。|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果可以重复使用在池中没有连接，请创建新的连接。|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知池 ID 已超时的驱动程序。|
