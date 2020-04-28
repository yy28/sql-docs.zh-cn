---
title: SQLConnect |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4e411d37f56090aff0de4d92a433dc61f95cd66
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302572"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。 有关 Spn 的详细信息，请参阅[&#40;ODBC&#41;的客户端连接中的服务主体名称 &#40;spn&#41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLConnect 支持  
 有关使用**SQLConnect**连接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]群集的详细信息，请参阅[高可用性和灾难恢复的 SQL Server Native Client 支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLConnect 函数](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
