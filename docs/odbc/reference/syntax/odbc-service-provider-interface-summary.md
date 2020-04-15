---
title: ODBC 服务提供商接口摘要 |微软文档
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
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298894"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 服务提供程序接口摘要
下表描述了 ODBC 服务提供商接口功能。 有关每个函数的语法和语义的详细信息，请参阅[ODBC 服务提供商接口 （SPI） 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
|函数名称|目标|  
|-------------------|-------------|  
|[SQLSetConnectattrFordbcinfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|与[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同，但它在连接信息令牌上而不是在连接句柄上设置属性。|  
|[SQLSet驱动程序连接信息](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|将连接字符串设置到应用程序的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)调用的连接信息令牌中。|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|将数据源、用户 ID 和密码设置到应用程序的[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用的连接信息令牌中。|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|检索池 ID。|  
|[SQLRate 连接](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|确定驱动程序是否可以重用连接池中的现有连接。|  
|[SQLPool连接](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|如果池中无法重用连接，则创建新连接。|  
|[SQL 清理连接池 ID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|通知驱动程序池 ID 已超时。|
