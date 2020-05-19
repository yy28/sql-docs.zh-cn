---
title: 对 ODBC 游标使用自动提取 |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a15cc12787f5a7d05699737772e7478d57b6f6e8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705602"
---
# <a name="using-autofetch-with-odbc-cursors"></a>通过 ODBC 游标使用自动提取
  当连接到实例时 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序支持使用任何服务器游标类型时的自动提取选项。 使用自动提取，打开游标的**SQLExecute**或**SQLExecDirect**函数也具有隐式[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)（SQL_FIRST）函数。 组成第一个行集的行将作为语句执行的一部分返回给绑定应用程序变量，并通过网络将另一个往返保存到服务器。 启用自动提取选项后，不支持[SQLGetData](../../native-client-odbc-api/sqlgetdata.md) ;结果集列必须绑定到程序变量。  
  
 应用程序通过对 SQL_CO_AF 设置特定于驱动程序的 SQL_SOPT_SS_CURSOR_OPTIONS 语句属性请求自动提取。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;的游标编程详细信息 &#40;](cursor-programming-details-odbc.md)  
  
  
