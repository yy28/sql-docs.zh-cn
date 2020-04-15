---
title: 线程支持（可视化福克斯Pro ODBC驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303078"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>线程支持（Visual FoxPro ODBC 驱动程序）
可视化 FoxPro ODBC 驱动程序是线程安全的。 对环境句柄 （*hen）、* 连接句柄 （*hdbc*） 和语句句柄 （*hstmt*） 的访问被包装在适当的信号量中，以防止其他进程访问并可能更改驱动程序的内部数据结构。  
  
 在多线程应用程序中，可以通过在单独的线程上调用[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)来取消在*hstmt*上同步运行的函数。  
  
 使用渐进式提取时，驱动程序使用单独的线程来获取数据。 要对数据源使用逐行提取，请在[ODBC Visual FoxPro 安装程序对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)**的后台复选框中选择"提取数据**"，或在连接字符串中使用后台提取属性关键字。 避免在从多线程应用程序调用驱动程序时使用后台提取。 有关连接字符串属性关键字的信息，请参阅[使用连接字符串](../../odbc/microsoft/using-connection-strings.md)。  
  
 有关线程和**SQLCancel**的详细信息，请参阅*ODBC 程序员参考*中的[SQLCancel。](../../odbc/reference/syntax/sqlcancel-function.md)
