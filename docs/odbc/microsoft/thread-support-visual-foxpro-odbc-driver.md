---
title: "线程支持 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd540c727f1e8a77dbb6d8201715c213ff688909
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>线程支持 （Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序是线程安全的。 访问环境句柄 (*当*)，连接句柄 (*hdbc*)，和语句句柄 (*hstmt*) 包装在适当的信号量，以防止其他进程访问并可能更改驱动程序的内部数据结构。  
  
 在多线程应用程序中，你可以取消正在同步函数*hstmt*通过调用[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)在单独线程上。  
  
 驱动程序使用一个单独的线程使用渐进式提取时提取数据。 若要使用渐进式提取的数据源，选择**提取数据，在后台**上的复选框[ODBC Visual FoxPro 安装程序对话框中](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或在你的连接中使用 BackgroundFetch 属性关键字字符串。 避免当多线程应用程序中调用该驱动程序时使用背景提取。 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
 有关线程的详细信息和**SQLCancel**，请参阅[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md)中*ODBC 程序员参考*。

