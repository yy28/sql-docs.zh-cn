---
title: 延迟缓冲区 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305978"
---
# <a name="deferred-buffers"></a>延迟的缓冲区
*延迟缓冲区*是其值在函数调用中指定*后*某个时间使用该缓冲区的缓冲区。 例如 **，SQLBind参数**用于将数据缓冲区与 SQL 语句中的参数关联或*绑定*。 应用程序指定参数的编号，并传递缓冲区的地址、字节长度和类型。 驱动程序保存此信息，但不检查缓冲区的内容。 稍后，当应用程序执行语句时，驱动程序检索信息并使用它检索参数数据并将其发送到数据源。 因此，将延迟缓冲区中数据的输入。 由于延迟缓冲区在一个函数中指定，在另一个函数中使用，因此在驱动程序仍希望它存在时释放延迟缓冲区是应用程序编程错误;有关详细信息，请参阅本节后面的[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 输入缓冲区和输出缓冲区都可以延迟。 下表总结了延迟缓冲区的使用。 请注意，绑定到结果集列的延迟缓冲区是使用**SQLBindCol**指定的，而绑定到 SQL 语句参数的延迟缓冲区则使用**SQLBind 参数**指定。  
  
|缓冲区使用|类型|使用|使用者|  
|----------------|----------|--------------------|-------------|  
|发送输入参数的数据|延迟输入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|发送数据以更新或插入结果集中的行|延迟输入|**SQLBindCol**|**SQLSetPos**|  
|返回输出和输入/输出参数的数据|延迟输出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|返回结果集数据|延迟输出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
