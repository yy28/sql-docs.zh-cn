---
title: 桌面数据库驱动程序的历史记录 |微软文档
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
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304978"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面数据库驱动程序的历史记录
下表显示了桌面数据库驱动程序版本历史记录。  
  
|版本|发布日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|使用了 PageAhead 软件生成的 SIMBA 查询处理器。 SIMBA 接收了 ODBC 呼叫和 SQL 语句，将它们处理到 Microsoft Jet 可安装的 ISAM 调用中，然后调用 Microsoft Jet ISAM 调度层来加载并调用适当的可安装 ISAM 驱动程序。|  
|2.0|1994年12月|与 ODBC 2.0 一起使用，显著扩展了 ODBC 功能。 版本 2.0 的主要变化是 Microsoft Jet 数据库引擎取代了 SIMBA 查询处理器。 借助 Microsoft Jet 数据库引擎，桌面数据库驱动程序与 Microsoft Jet 可安装的 ISAM 驱动程序和 Microsoft Access 技术集成得更紧密。 显著增强：：<br /><br /> - 对可滚动游标的本机支持。<br />- 对外部联接的本机支持、可异构联接和事务。<br />- 微软 Windows NT 的驱动程序的 32 位版本。|  
|3.0|1995年10月|为 Windows 95 和 Windows NT 工作站或 NT 服务器 3.51 提供支持。 此版本中仅包含 32 位驱动程序;Windows 版本 3.1 的 16 位驱动程序已被删除。|  
|3.5|1996年10月|这些驱动程序支持双字节字符集 （DBCS），与以前的版本更适合 Internet 应用程序使用，并且适合使用文件数据源名称 （DSN）。 Microsoft Access 驱动程序以 RISC 版本发布，用于适用于 Windows 95/98 和 Windows NT 3.51 及更高版本的操作系统的 Alpha 平台。|  
|4.0|1998年末|支持 Microsoft 喷气引擎 Unicode 格式以及早期版本的 ANSI 格式的兼容性。|  
  
> [!NOTE]  
>  版本3.5驱动程序的设计与 ODBC2 配合使用。*x*. . 虽然它们也使用 ODBC 3.0，但它们不支持所有 ODBC 3.0 功能。 有关这些驱动程序如何与 ODBC 3.0 配合使用的详细信息，请参阅[向后兼容性和标准合规性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
