---
title: 延迟的缓冲区 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5273f48c96039e543e24c2945cd5cda14d352e6d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="deferred-buffers"></a>延迟的缓冲区
A*延迟的缓冲区*是在某个时间使用其值*后*函数调用中指定。 例如， **SQLBindParameter**用于将相关联，或*绑定，*具有 SQL 语句中的参数的数据缓冲区。 应用程序指定的参数数目，并传递地址、 字节长度和类型的缓冲区。 驱动程序将保存此信息，但不检查缓冲区的内容。 更高版本，当应用程序执行语句，该驱动程序检索的信息并使用它检索参数数据并将其发送到数据源。 因此，延迟的输入缓冲区中的数据。 延迟的缓冲区是一个函数中指定，并且用于另一个，因为它是对应用程序编程错误驱动程序仍希望存在; 将释放延迟的缓冲区有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)，本部分中更高版本。  
  
 输入和输出缓冲区可以被推迟。 下表概述了延迟的缓冲区的使用。 请注意，用指定绑定到结果集列的延迟的缓冲区**SQLBindCol**，并使用指定绑定到 SQL 语句参数的延迟的缓冲区**SQLBindParameter**。  
  
|缓冲区使用|类型|使用指定|使用者|  
|----------------|----------|--------------------|-------------|  
|用于输入参数发送数据|延迟的输入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|发送要更新或插入行在结果中的数据设置|延迟的输入|**SQLBindCol**|**SQLSetPos**|  
|对于输出参数和输入/输出参数返回数据|输出延迟|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|返回结果集数据|输出延迟|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
