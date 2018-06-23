---
title: 批处理存储的过程调用 |Microsoft 文档
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
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd3d7fca3dc22d20c9aeadfc3b60fa41fa64f895
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026764"
---
# <a name="batching-stored-procedure-calls"></a>批处理存储过程调用
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序自动批处理到服务器时相应的存储的过程调用。 只有在使用 ODBC CALL 转义序列时驱动程序才执行此操作；它并不为 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 语句执行此操作。 批处理存储过程调用可以减少到服务器的往返数目，因此可以显著提高性能。  
  
 在执行包含多个 ODBC CALL 转义序列的批处理时，驱动程序批处理对服务器的过程调用。 它还在绑定参数数组用于 ODBC CALL 转义序列时批处理过程调用。 例如，如果你使用任一按行或列的参数绑定来绑定到 ODBC 调用 SQL 语句中的参数的带有五个元素的数组时**SQLExecute**或**SQLExecDirect**调用时，该驱动程序将发送到服务器的五个过程调用带有的单个批次。  
  
## <a name="see-also"></a>请参阅  
 [运行存储过程](running-stored-procedures.md)  
  
  