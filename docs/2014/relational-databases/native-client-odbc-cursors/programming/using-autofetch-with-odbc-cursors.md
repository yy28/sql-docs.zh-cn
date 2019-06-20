---
title: 通过 ODBC 游标使用自动提取 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 343975c2c6ad39c67dcd10c0d55886d21e69f3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711555"
---
# <a name="using-autofetch-with-odbc-cursors"></a>通过 ODBC 游标使用自动提取
  连接到的实例时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，则[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用任何服务器游标类型时，Native Client ODBC 驱动程序支持自动提取选项。 启用了自动提取， **SQLExecute**或**SQLExecDirect**打开游标的函数也具有隐式[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 函数。 组成第一个行集的行将作为语句执行的一部分返回给绑定应用程序变量，并通过网络将另一个往返保存到服务器。 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)时不支持自动提取选项，则启用; 将结果集列必须绑定到程序变量。  
  
 应用程序通过对 SQL_CO_AF 设置特定于驱动程序的 SQL_SOPT_SS_CURSOR_OPTIONS 语句属性请求自动提取。  
  
## <a name="see-also"></a>请参阅  
 [游标编程详细信息&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
