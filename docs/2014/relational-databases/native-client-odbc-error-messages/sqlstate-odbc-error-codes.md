---
title: SQLSTATE （ODBC 错误代码） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6dbffb716887ed3ad7f5a34d12e806dedd713a30
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089814"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）
  SQLSTATE 提供与警告或错误的原因有关的详细信息。 在数据中出现的错误源检测到并返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将返回本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到，ODBC 错误代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将返回 SQLSTATE 42000 （"语法错误或访问冲突"）。 对于由驱动程序检测到的错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将生成相应的 SQLSTATE。  
  
 有关状态错误代码的详细信息，请参阅下面的主题：  
  
-   [附录 A：ODBC 错误代码](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 映射](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>请参阅  
 [处理错误和消息](handling-errors-and-messages.md)  
  
  
