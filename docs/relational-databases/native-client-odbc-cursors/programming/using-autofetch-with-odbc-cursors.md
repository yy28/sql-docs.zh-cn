---
title: 对 ODBC 游标使用自动提取 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98ac32d37598c3234a6a02320139e537b694ca07
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784251"
---
# <a name="using-autofetch-with-odbc-cursors"></a>通过 ODBC 游标使用自动提取
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  当连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序在使用任何服务器游标类型时都支持自动提取选项。 使用自动提取，打开游标的**SQLExecute**或**SQLExecDirect**函数也具有隐式[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)（SQL_FIRST）函数。 组成第一个行集的行将作为语句执行的一部分返回给绑定应用程序变量，并通过网络将另一个往返保存到服务器。 启用自动提取选项后，不支持[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) ;结果集列必须绑定到程序变量。  
  
 应用程序通过对 SQL_CO_AF 设置特定于驱动程序的 SQL_SOPT_SS_CURSOR_OPTIONS 语句属性请求自动提取。  
  
## <a name="see-also"></a>另请参阅  
 [游标编程详细&#40;信息 ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
