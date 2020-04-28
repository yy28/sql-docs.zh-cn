---
title: 安装访问 SQL Server 迁移助手（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: cbbb7ed7a20937d9963af7080fb16be4f6c78da5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "79111905"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安装访问 SQL Server 迁移助手（AccessToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用基于 Windows Installer 的向导安装访问的迁移助手（SSMA）。 本主题提供了有关安装先决条件的信息、SSMA 的最新版本的链接，以及安装、授权、卸载和升级 SSMA 的说明。  
  
## <a name="prerequisites"></a>先决条件  
安装 SSMA 之前，请确保你的系统满足以下要求：  
  
-   Windows 7 或更高版本，或者 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本4.0 或更高版本。 .NET Framework 版本4.0 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品光盘上提供，并使用[Microsoft .NET 指南](https://docs.microsoft.com/dotnet/framework/)中的信息。
  
-   在承载要将数据库对象和数据迁移到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure DB 目标实例的计算机上，访问和足够的权限。  
  
-   Microsoft 数据访问对象（DAO）提供程序版本12.0 或14.0。 可以从 Microsoft Office 2010/2007 产品安装 DAO 提供程序，也可以从 Microsoft 网站下载。  
  
-   SQL Server 的本机访问客户端（SNAC）版本10.5 及更高版本，以便迁移到 SQL Azure。 你可以从[Microsoft® SQL Server® 2008 R2 功能包](https://www.microsoft.com/download/details.aspx?id=44272)获取最新版本的 SNAC  
  
-   4 GB RAM （建议使用）。  
  
## <a name="installing-ssma"></a>安装 SSMA  
SSMA 是一款可以从 Web 下载的工具。 若要下载最新版本，请参阅[SQL Server 迁移助手下载 "页](https://aka.ms/ssmaforaccess)。  
  
下载最新版本后，必须从中提取安装文件，然后才能安装 SSMA。

> [!IMPORTANT]  
> -   安装新版本之前，请卸载所有以前版本的 SSMA 以进行访问。  
  
**安装 SSMA**  
  
1.  双击 "SSMA" 以访问 " *n*"，其中*n*是生成号。  
  
2.  在欢迎页上，单击 "**下一步**"。  
  
    如果未安装必备组件，则会出现一条消息，指示必须首先安装所需的组件。 请确保已安装所有必备组件，然后再次运行安装程序。  
  
3.  阅读最终用户许可协议;如果同意，请选择 "**我接受协议**"，然后单击 "**下一步**"。  
  
4.  在 "选择安装类型" 页上，单击 "**典型**"。  
  
5.  单击“安装”  。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server 迁移助手用于访问。  
  
## <a name="uninstalling-ssma-for-access"></a>正在卸载 SSMA 以进行访问  
使用控制面板中的 "**添加或删除程序**" 卸载 SSMA。 请注意，卸载程序并不会删除 SSMA 项目文件或日志文件。  
  
**卸载 SSMA**  
  
1.  依次单击“开始”****、“控制面板”****，然后单击“添加或删除程序”****。  
  
2.  选择 " **Microsoft SQL Server 迁移助手进行访问**"，然后单击 "**删除**"。  
  
## <a name="upgrading-to-a-later-version"></a>升级到更高版本  
如果要升级到 SSMA 的更高版本，则必须先卸载 SSMA 以进行访问，然后再安装较新版本。 按照卸载 SSMA for Access 部分的说明完成此过程。  
  
如果你打开在 SSMA for Access 的早期版本中创建的项目，则 SSMA 会询问你是否要将该项目转换为较新的版本。 单击 **"是"** 以使用 SSMA 的较新版本中的项目。  
  
## <a name="see-also"></a>另请参阅  
[准备要迁移的 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)  
[将 Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[将访问应用程序链接到 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
