---
title: 本机错误号 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63223499"
---
# <a name="native-error-numbers"></a>本机错误号
  对于数据源中发生的错误（由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 驱动程序返回由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回的本机错误号。 对于驱动程序检测到的错误， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序返回本机错误号0。 有关本机错误号列表的详细信息，请参阅中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **master**数据库中**sysmessages**系统表的错误列。  
  
 有关状态错误代码的信息，请参阅[SQLSTATE &#40;ODBC 错误代码&#41;](sqlstate-odbc-error-codes.md)。 对于网络库返回的错误，本机错误号来自于基础网络软件。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](handling-errors-and-messages.md)  
  
  
