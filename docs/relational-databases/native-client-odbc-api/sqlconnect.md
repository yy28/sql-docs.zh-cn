---
title: SQLConnect |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cd6129ae9df48dbc30bc59e44b8880f33b1420bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942312"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。 有关 Spn 的详细信息，请参阅[服务主体名称 & #40;Spn & #41;在客户端连接 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLConnect 支持  
 有关详细信息使用**SQLConnect**连接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]群集，请参阅[高可用性、 灾难恢复的 SQL Server Native Client Support](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLConnect 函数](http://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
