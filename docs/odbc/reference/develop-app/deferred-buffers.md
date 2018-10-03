---
title: 延迟的缓冲区 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b071494697d21a37f4420889a8f60cc35fe3d8b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797195"
---
# <a name="deferred-buffers"></a>延迟的缓冲区
一个*延迟的缓冲区*是一个其值用于在某个时间*后*函数调用中指定。 例如， **SQLBindParameter**用于将相关联，或*绑定，* 具有中的 SQL 语句的参数的数据缓冲区。 应用程序指定参数的编号，并通过地址、 字节长度和类型的缓冲区。 驱动程序将保存此信息，但不检查缓冲区的内容。 更高版本，当应用程序执行该语句，该驱动程序检索信息，并使用它来检索参数数据并将其发送到数据源。 因此，将延迟的输入缓冲区中的数据。 因为延迟的缓冲区是在一个函数中指定，在另一个中使用，它是编程错误的应用程序以释放延迟的缓冲区，而该驱动程序仍期望它可存在;有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)，在本部分中更高版本。  
  
 可以延迟输入和输出缓冲区。 下表概述了延迟的缓冲区的使用。 请注意，使用指定绑定到结果集列的延迟的缓冲区**SQLBindCol**，并使用指定绑定到 SQL 语句参数的延迟的缓冲区**SQLBindParameter**。  
  
|缓冲区使用|类型|使用指定|使用者|  
|----------------|----------|--------------------|-------------|  
|发送输入参数的数据|延迟的输入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|若要更新或插入行在结果中将数据发送设置|延迟的输入|**SQLBindCol**|**SQLSetPos**|  
|对于输出参数和输入/输出参数返回数据|延迟的输出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|返回结果集数据|延迟的输出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
