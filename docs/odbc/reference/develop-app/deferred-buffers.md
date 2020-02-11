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
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076836"
---
# <a name="deferred-buffers"></a>延迟的缓冲区
*延迟缓冲区*是指在函数调用中指定一个时间*后*在某个时间使用该值的缓冲区。 例如，使用**SQLBindParameter**可将数据缓冲区与 SQL 语句*中的参数*相关联。 应用程序指定参数号，并传递缓冲区的地址、字节长度和类型。 驱动程序将保存此信息，但不检查缓冲区的内容。 稍后，当应用程序执行该语句时，驱动程序会检索信息，并使用它检索参数数据并将其发送到数据源。 因此，缓冲区中的数据输入将延迟。 由于延迟缓冲区是在一个函数中指定并在另一个函数中使用的，因此，当驱动程序仍预期存在延迟缓冲区时，它是一个应用程序编程错误，有关详细信息，请参阅本节后面的[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 输入和输出缓冲区都可以推迟。 下表总结了延迟缓冲区的用法。 请注意，绑定到结果集列的延迟缓冲区是通过**SQLBindCol**指定的，并且绑定到 SQL 语句参数的延迟缓冲区是通过**SQLBindParameter**指定的。  
  
|缓冲区使用|类型|指定的|使用者|  
|----------------|----------|--------------------|-------------|  
|发送输入参数的数据|延迟输入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|发送数据以更新或在结果集中插入行|延迟输入|**SQLBindCol**|**SQLSetPos**|  
|返回输出和输入/输出参数的数据|延迟的输出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|返回结果集数据|延迟的输出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
