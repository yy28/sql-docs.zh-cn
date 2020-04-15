---
title: 驱动程序体系结构概述 |微软文档
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
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303458"
---
# <a name="driver-architecture-overview"></a>驱动程序体系结构概述
Microsoft Visual FoxPro ODBC 驱动程序是一个 32 位驱动程序，使您能够通过开放数据库连接 （ODBC） 界面打开和查询 Microsoft Visual FoxPro 数据库或 FoxPro 表。 您可以使用以下类型的应用程序访问 FoxPro 数据：  
  
-   使用微软查询与 ODBC 通信的微软 Office 应用程序，如 Microsoft Excel 或 Microsoft Word。  
  
-   使用 ODBC SDK API 在 Microsoft 视觉C++或 C 编写的应用程序。  
  
-   以 Microsoft 可视化基本版或 Microsoft 应用程序视觉基本版编写的应用程序。  
  
 在每种情况下，信息请求都使用 ODBC API。 ODBC 驱动程序管理器与 Visual FoxPro ODBC 驱动程序合作，从 FoxPro 表和数据库打开和检索数据。  
  
 体系结构在下图中表示：  
  
 ![显示 ODBC 驱动程序体系结构](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 本部分包含以下主题。  
  
-   [Visual FoxPro 术语](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安装和配置可视化福克斯Pro ODBC驱动程序](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC 驱动程序](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
