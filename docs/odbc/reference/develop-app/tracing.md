---
description: 跟踪
title: 跟踪 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25a7a08fb5c5d2fb203151fb014bdc0edfd25746
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487480"
---
# <a name="tracing"></a>跟踪
ODBC 驱动程序管理器具有一个跟踪工具，该工具允许将 ODBC 应用程序发出的函数调用序列记录并转录到日志文件中。 跟踪由跟踪 DLL 执行，该 DLL 捕获应用程序和驱动程序管理器之间以及驱动程序管理器和驱动程序之间的调用。 这种跟踪方法取代了 odbc*2.X 驱动程序* 管理器执行的跟踪，以及 odbc SPY 在 odbc 2.x 中*执行的跟踪* 。  
  
 本部分包含以下主题。  
  
-   [跟踪 DLL](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [跟踪文件](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [启用跟踪](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [动态跟踪](../../../odbc/reference/develop-app/dynamic-tracing.md)
