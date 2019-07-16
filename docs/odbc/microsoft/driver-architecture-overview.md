---
title: 驱动程序体系结构概述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071921"
---
# <a name="driver-architecture-overview"></a>驱动程序体系结构概述
Microsoft Visual FoxPro ODBC 驱动程序是一个 32 位驱动程序，可用于打开和查询 Microsoft Visual FoxPro 数据库或多个 FoxPro 表通过开放式数据库连接 (ODBC) 接口。 您可以访问使用以下类型的应用程序的 FoxPro 数据：  
  
-   使用 Microsoft 查询与 ODBC 进行通信的 Microsoft Office 应用程序，如 Microsoft Excel 或 Microsoft Word。  
  
-   Microsoft 的视觉对象中编写的应用程序C++或使用 ODBC SDK API 的 C。  
  
-   在 Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 中编写的应用程序。  
  
 在每种情况下，请求的信息使用 ODBC API。 ODBC 驱动程序管理器适用于 Visual FoxPro ODBC 驱动程序打开，并从 FoxPro 表和数据库中检索数据。  
  
 下图中表示体系结构：  
  
 ![显示 ODBC 驱动程序体系结构](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 本部分包含以下主题。  
  
-   [Visual FoxPro 术语](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安装和配置 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
