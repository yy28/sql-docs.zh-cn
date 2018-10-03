---
title: 线程支持 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77187802bb57a832263ec2070564754e87f21345
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758865"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>线程支持（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序是线程安全的。 访问环境句柄 (*hen*)，连接句柄 (*hdbc*)，和语句句柄 (*hstmt*) 封装在适当的信号量，以防止其他进程从访问，从而可能会改变，驱动程序的内部数据结构。  
  
 可以在多线程应用程序中，取消同步运行的函数*hstmt*通过调用[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)单独的线程上。  
  
 驱动程序使用单独的线程使用渐进式提取时提取数据。 若要使用渐进式提取的数据源，选择**提取背景中的数据**上的复选框[ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或在你的连接中使用 BackgroundFetch 属性关键字字符串。 避免当多线程应用程序中调用该驱动程序时使用后台获取。 有关连接字符串属性关键字的信息，请参阅[连接字符串使用](../../odbc/microsoft/using-connection-strings.md)。  
  
 有关线程的详细信息和**SQLCancel**，请参阅[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md)中*ODBC 程序员参考*。
