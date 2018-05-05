---
title: 安装 SQL Server Migration Assistant 用于访问 (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
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
ms.openlocfilehash: 4232c955646b44be8c1d41a9095146a47aa75e97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安装访问 (AccessToSQL) 的 SQL Server 迁移的助手
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 使用基于 Windows Installer 的向导，可安装 migration Assistant (SSMA) 的访问。 本主题提供有关安装、 许可、 卸载和升级 SSMA 有关安装先决条件的信息到 SSMA，最新版本的链接和说明。  
  
## <a name="prerequisites"></a>必要條件  
在安装 SSMA 之前，请确保你的系统满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本 4.0 或更高版本。 .NET Framework 版本 4.0 位于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产品光盘，以及通过使用中的信息[Microsoft.NET 指南](https://docs.microsoft.com/en-us/dotnet/framework/)。
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]到将迁移数据库对象和数据的 SQL Azure DB。  
  
-   Microsoft 数据访问对象 (DAO) 提供程序版本 12.0 或 14.0。 你可以从 Microsoft Office 2010/2007年产品安装 DAO 提供程序，或从 Microsoft 网站上下载它。  
  
-   SQL Server Native 访问 Client (SNAC) 10.5 版和更高版本迁移到 SQL Azure。 你可以获取最新版本从 SNAC [Microsoft® SQL Server® 2008 R2 功能包](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB RAM （推荐）。  
  
## <a name="installing-ssma"></a>安装 SSMA  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmaforaccess)。  
  
下载最新版本之后，你必须提取中的安装文件，然后才能安装 SSMA。

> [!IMPORTANT]  
> -   请在安装新版本之前卸载所有以前的 SSMA for Access 版本。  
  
**若要安装 SSMA**  
  
1.  双击 SSMA for Access *n*.msi，其中*n*为内部版本号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果你没有安装的先决条件，一条消息将出现，指示你必须首先安装所需的组件。 请确保已安装所有必备条件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议;如果同意，请选中**我接受协议**，然后单击**下一步**。  
  
4.  在选择安装类型页上，单击**典型**。  
  
5.  单击 **“安装”**。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for Access。  
  
## <a name="uninstalling-ssma-for-access"></a>卸载 SSMA for Access  
通过使用卸载 SSMA**添加或删除程序**控制面板中。 请注意，卸载程序不删除 SSMA 项目文件或日志文件。  
  
**若要卸载 SSMA**  
  
1.  单击**启动**，单击**控制面板**，然后单击**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Access**，然后单击**删除**。  
  
## <a name="upgrading-to-a-later-version"></a>升级到更高版本  
如果你想要升级到更高版本的 SSMA for Access，您必须先卸载 SSMA for Access，然后安装较新版本。 按照中卸载 SSMA 访问部分，若要完成此过程的说明。  
  
如果打开 SSMA for Access 的早期版本中创建的项目，则会要求 SSMA，如果你想要将项目转换为较新版本。 单击**是**用于 SSMA 的较新版本中的项目。  
  
## <a name="see-also"></a>另请参阅  
[为迁移准备的 Access 数据库](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
