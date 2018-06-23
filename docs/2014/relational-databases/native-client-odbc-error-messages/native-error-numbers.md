---
title: 本机错误数字 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: faee9067ccf8f60a4b7dade849a0a987b5c07bd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123847"
---
# <a name="native-error-numbers"></a>本机错误号
  为数据源中发生的错误 (由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序返回到它返回的本机错误号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关驱动程序，检测到的错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序返回本机错误号 0。 有关的本机错误数字列表的详细信息，请参阅的错误列**sysmessages**系统表位于**master**数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 有关状态错误代码的信息，请参阅[SQLSTATE &#40;ODBC 错误代码&#41;](sqlstate-odbc-error-codes.md)。 对于网络库返回的错误，本机错误号来自于基础网络软件。  
  
## <a name="see-also"></a>请参阅  
 [处理错误和消息](handling-errors-and-messages.md)  
  
  