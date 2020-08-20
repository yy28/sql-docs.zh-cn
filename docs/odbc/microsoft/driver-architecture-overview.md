---
description: 驱动程序体系结构概述
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d71a2c28825ee8c7d4e12e047234f3e336b339e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466439"
---
# <a name="driver-architecture-overview"></a>驱动程序体系结构概述
Microsoft Visual FoxPro ODBC 驱动程序是一个32位驱动程序，使您能够通过开放式数据库连接 (ODBC) 接口打开和查询 Microsoft Visual FoxPro 数据库或 FoxPro 表。 您可以使用以下类型的应用程序访问 FoxPro 数据：  
  
-   一个 Microsoft Office 的应用程序，如 Microsoft Excel 或 Microsoft Word，它们使用 Microsoft Query 与 ODBC 通信。  
  
-   使用 ODBC SDK API Microsoft Visual C++ 或 C 编写的应用程序。  
  
-   使用 Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 编写的应用程序。  
  
 在每种情况下，对信息的请求均使用 ODBC API。 ODBC 驱动程序管理器与 Visual FoxPro ODBC 驱动程序一起使用，以打开和检索来自 FoxPro 表和数据库的数据。  
  
 下图显示了此体系结构：  
  
 ![显示 ODBC 驱动程序体系结构](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 本部分包含以下主题。  
  
-   [Visual FoxPro 术语](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安装和配置 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
