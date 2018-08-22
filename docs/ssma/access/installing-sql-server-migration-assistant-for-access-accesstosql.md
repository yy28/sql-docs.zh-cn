---
title: 安装 SQL Server 迁移助手进行访问 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dacd6634e57043ca53dfceb9bf3d793b35c90a47
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395454"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安装 SQL Server 迁移助手进行访问 (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移助手 (SSMA) for Access 使用的基于 Windows Installer 的向导进行安装。 本主题提供有关安装、 许可、 卸载和升级 SSMA 安装先决条件、 SSMA，最新版本的链接的信息和说明。  
  
## <a name="prerequisites"></a>必要條件  
安装 SSMA 之前，请确保你的系统满足以下要求：  
  
-   Windows 7 或更高版本或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本 4.0 或更高版本。 .NET Framework 版本 4.0 是上可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品光盘，并通过使用中的信息[Microsoft.NET 指南](https://docs.microsoft.com/dotnet/framework/)。
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure DB 向其将迁移数据库对象和数据。  
  
-   Microsoft 数据访问对象 (DAO) 提供程序版本 12.0 或 14.0。 可以从 Microsoft Office 2010/2007年产品安装 DAO 提供程序或从 Microsoft 网站上下载它。  
  
-   SQL Server Native Access Client (SNAC) 版本 10.5 及更高版本迁移到 SQL Azure。 你可以获取最新版本从 SNAC [Microsoft® SQL Server® 2008 R2 功能包](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB RAM （推荐）。  
  
## <a name="installing-ssma"></a>安装 SSMA  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmaforaccess)。  
  
下载最新版本后，您必须提取中的安装文件，然后才能安装 SSMA。

> [!IMPORTANT]  
> -   请安装最新版本之前卸载所有以前版本的 SSMA for Access。  
  
**若要安装的 SSMA**  
  
1.  双击 SSMA for Access *n*.msi，其中*n*是生成号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，指示您必须首先安装所需的组件。 请确保已安装所有必备组件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议;如果同意，请选择**我接受协议**，然后单击**下一步**。  
  
4.  在选择安装类型页上单击**典型**。  
  
5.  单击 **“安装”**。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for Access。  
  
## <a name="uninstalling-ssma-for-access"></a>卸载 SSMA for Access  
使用卸载 SSMA**添加或删除程序**控制面板中。 请注意，卸载该程序不删除 SSMA 项目文件或日志文件。  
  
**若要卸载的 SSMA**  
  
1.  单击**启动**，单击**控制面板**，然后单击**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Access**，然后单击**删除**。  
  
## <a name="upgrading-to-a-later-version"></a>升级到更高版本  
如果你想要升级到更高版本的 SSMA for Access，您必须首先卸载 SSMA for Access，然后安装较新版本。 按照卸载 SSMA 中访问部分，若要完成此过程的说明。  
  
如果您打开 SSMA for Access 的早期版本中创建的项目，SSMA 询问您是否要将项目转换为较新版本。 单击**是**以使用较新版本的 SSMA 中的项目。  
  
## <a name="see-also"></a>另请参阅  
[为迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[链接到 SQL Server 访问应用程序](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
