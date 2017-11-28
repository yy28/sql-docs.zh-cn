---
title: "桌面数据库驱动程序的历史记录 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: beb79b003e6e36b195d781b071dde814c5265adc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面数据库驱动程序的历史记录
下表显示桌面数据库驱动程序版本历史记录。  
  
|版本|发布日期|Description|  
|-------------|------------------|-----------------|  
|1.0|年 8 月 1993|使用由 PageAhead 软件 SIMBA 查询处理器。 SIMBA 收到 ODBC 调用和 SQL 语句，处理到 Microsoft Jet 可安装 ISAM 调用，然后调用 Microsoft Jet ISAM 调度层以加载并调用适当的可安装 ISAM 驱动程序。|  
|2.0|年 12 月 1994|用于 ODBC 2.0，ODBC 功能，从而大大扩展。 在 2.0 版中的主要更改是，Microsoft Jet 数据库引擎替换 SIMBA 查询处理器。 使用 Microsoft Jet 数据库引擎时，桌面数据库驱动程序集成更紧密与 Microsoft Jet 可安装 ISAM 驱动程序和 Microsoft Access 技术。 中的重大增强功能：<br /><br /> 的可滚动游标本机支持。<br />的外部联接、 更新和异构性会联接和事务本机支持。<br />-32 位版本的 Microsoft Windows NT 的驱动程序。|  
|3.0|年 10 月 1995 1995年|提供了为 Windows 95 和 Windows NT 工作站或 NT Server 3.51 的支持。 唯一的 32 位驱动程序已包含在此版本;Windows 版本 3.1 的 16 位驱动程序已删除。|  
|3.5|年 10 月 1996|这些驱动程序已双字节字符集 (DBCS)-启用、 已更好地比以前版本中适用于与 Internet 应用程序一起使用并且容纳文件数据源名称 (Dsn) 的使用。 Microsoft Access 驱动程序中使用 Alpha 平台上为 Windows 95/98 和 Windows NT 3.51 和更高版本操作系统的 RISC 版本发布。|  
|4.0|后期 1998|提供对 Microsoft Jet 引擎 Unicode 格式以及 ANSI 格式的早期版本的兼容性支持。|  
  
> [!NOTE]  
>  Version3.5 驱动程序旨在使用 ODBC2。*x*。 虽然它们还能配合 ODBC 3.0，它们不支持所有 ODBC 3.0 功能。 有关这些驱动程序与 ODBC 3.0 的工作原理的详细信息，请参阅[向后兼容性和标准合规性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
