---
description: 桌面数据库驱动程序的历史记录
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80e8f1b52abac92ba09b97d35d45dfe0506963ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500320"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面数据库驱动程序的历史记录
下表显示了桌面数据库驱动程序版本历史记录。  
  
|版本|发布日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|使用 PageAhead 软件生成的 SIMBA 查询处理器。 SIMBA 收到了 ODBC 调用和 SQL 语句，将它们处理为 Microsoft Jet 可安装的 ISAM 调用，然后调用 Microsoft Jet ISAM 调度层来加载并调用合适的可安装的 ISAM 驱动程序。|  
|2.0|1994年12月|与 ODBC 2.0 一起使用，这大大扩展了 ODBC 功能。 版本2.0 的主要变化在于，Microsoft Jet 数据库引擎已替换 SIMBA 查询处理器。 使用 Microsoft Jet 数据库引擎，桌面数据库驱动程序与 Microsoft Jet 可安装的 ISAM 驱动程序和 Microsoft Access 技术紧密集成。 重要的增强功能：<br /><br /> -对可滚动游标的本机支持。<br />-对外部联接、可更新和异类联接以及事务的本机支持。<br />-32 位版本的 Microsoft Windows NT 驱动程序。|  
|3.0|1995年10月|提供对 Windows 95 和 Windows NT 工作站或 NT Server 3.51 的支持。 此版本中只包含32位驱动程序;Windows 版本3.1 的16位驱动程序已删除。|  
|3.5|1996年10月|这些驱动程序是双字节字符集 (DBCS) 启用，更适合与以前版本的 Internet 应用程序一起使用，并可将文件数据源名称的使用 (Dsn) 提供。 Microsoft Access 驱动程序以 RISC 版本发布，适用于适用于 Windows 95/98 和 Windows NT 3.51 及更高版本操作系统的 Alpha 平台。|  
|4.0|延迟1998|提供对 Microsoft Jet 引擎 Unicode 格式的支持以及早期版本的 ANSI 格式的兼容性。|  
  
> [!NOTE]  
>  3.5 版驱动程序设计为与 ODBC2 配合使用。*x*。 尽管它们也适用于 ODBC 3.0，但并不支持所有 ODBC 3.0 功能。 有关这些驱动程序如何与 ODBC 3.0 一起使用的详细信息，请参阅 [向后兼容性和标准符合性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
