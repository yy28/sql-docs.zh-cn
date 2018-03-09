---
title: "驱动程序体系结构概述 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2778161fa117e164a4c49e57a5511b0682507b37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="driver-architecture-overview"></a>驱动程序体系结构概述
Microsoft Visual FoxPro ODBC 驱动程序是可用于打开和查询 Microsoft Visual FoxPro 数据库或通过打开数据库连接 (ODBC) 界面 FoxPro 表的 32 位驱动程序。 你可以访问 FoxPro 数据使用以下类型的应用程序：  
  
-   使用 Microsoft 查询与 ODBC 进行通信的 Microsoft Office 应用，例如 Microsoft Excel 或 Microsoft Word。  
  
-   在 Microsoft Visual c + + 或使用 ODBC SDK API 的 C 中编写的应用程序。  
  
-   在 Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 中编写的应用程序。  
  
 在每种情况下，请求的信息使用 ODBC API。 ODBC 驱动程序管理器配合 Visual FoxPro ODBC 驱动程序以打开并从 FoxPro 表和数据库中检索数据。  
  
 在下图中表示体系结构：  
  
 ![显示的 ODBC 驱动程序体系结构](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 本部分包含以下主题。  
  
-   [Visual FoxPro 术语](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安装和配置 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
