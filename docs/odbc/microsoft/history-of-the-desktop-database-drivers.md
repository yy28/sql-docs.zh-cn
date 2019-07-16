---
title: 桌面数据库驱动程序的历史记录 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d225bac273558b928e3e8fd2f41bd121a723f6ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952372"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面数据库驱动程序的历史记录
下表显示了桌面数据库驱动程序版本历史记录。  
  
|Version|发布日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993 年 8 月|使用生成的 PageAhead 软件 SIMBA 查询处理器。 SIMBA 收到 ODBC 调用和 SQL 语句、 为 Microsoft Jet 的可安装 ISAM 调用，处理它们，然后调用 Microsoft Jet ISAM 调度层来加载并调用相应的可安装 ISAM 驱动程序。|  
|2.0|1994 年 12 月|与 ODBC 2.0，显著扩大 ODBC 功能一起使用。 在 2.0 版中的主要更改是 Microsoft Jet 数据库引擎替换 SIMBA 查询处理器。 使用 Microsoft Jet 数据库引擎，桌面数据库驱动程序集成更紧密 Microsoft Jet 可安装 ISAM 驱动程序和 Microsoft Access 技术。 介绍了重要的增强功能：<br /><br /> 的对于可滚动游标本机支持。<br />的外部联接、 可更新与异类联接和事务本机支持。<br />-32 位版本的驱动程序的 Microsoft Windows NT。|  
|3.0|1995 年 10 月|提供对 Windows 95 和 Windows NT Workstation 或 NT Server 3.51 的支持。 仅 32 位驱动程序包含在此版本中;已删除的 Windows 版本 3.1 的 16 位驱动程序。|  
|3.5|1996 年 10 月|这些驱动程序是双字节字符集 (DBCS)-启用、 已更好地适用于与 Internet 应用程序一起使用比以前版本，并且允许使用的文件数据源名称 (Dsn)。 Microsoft Access 驱动程序中使用 Alpha 平台上为 Windows 95/98 和 Windows NT 3.51 和更高版本操作系统的 RISC 版本发布。|  
|4.0|后期 1998|为 Microsoft Jet 引擎 Unicode 格式，以及 ANSI 格式的早期版本的兼容性提供支持。|  
  
> [!NOTE]  
>  Version3.5 驱动程序已设计用于 ODBC2。*x*。 尽管也适用于 ODBC 3.0，但它们不支持所有 ODBC 3.0 功能。 这些驱动程序如何使用 ODBC 3.0 的详细信息，请参阅[向后兼容性和标准符合性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
