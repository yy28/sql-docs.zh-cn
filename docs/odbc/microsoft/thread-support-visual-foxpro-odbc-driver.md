---
title: 线程支持（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303078"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>线程支持（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序是线程安全的。 对环境句柄（*h)*）、连接句柄（*hdbc*）和语句句柄（*hstmt*）的访问将包装在适当的信号量中，以防止其他进程访问并可能更改驱动程序的内部数据结构。  
  
 在多线程应用程序中，可以通过在单独的线程上调用[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)来取消在*hstmt*上同步运行的函数。  
  
 使用渐进式提取时，驱动程序将使用一个单独的线程来提取数据。 若要对数据源使用渐进式提取，请在 " [ODBC Visual FoxPro 安装程序" 对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中选择 "**以后台提取数据**" 复选框，或在连接字符串中使用 BackgroundFetch 特性关键字。 从多线程应用程序调用驱动程序时，请避免使用后台提取。 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
 有关线程和**SQLCancel**的详细信息，请参阅*ODBC 程序员参考*中的[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) 。
