---
title: 安装 SQL Server Native Client |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4023294d52724e5cd132ab4a47b8b8e7f910e3a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394229"
---
# <a name="installing-sql-server-native-client"></a>安装 SQL Server Native Client
  Microsoft[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装时安装 Native Client 11.0 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。 没有 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client。 有关详细信息，请参阅[What's New in SQL Server Native Client](../sql-server-native-client.md)。 你还可以从 SQL Server 2012 功能包网页获取 sqlncli.msi。 若要下载 SQL Server Native Client 的最新版本，请转到[Microsoft® SQL Server® 2012 SP2 功能包](http://www.microsoft.com/en-us/download/details.aspx?id=43339)。 如果以前版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早于的计算机上，也安装 SQL Server 2012 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 将与早期版本并行安装。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 文件（sqlncli11.dll、sqlnclir11.rll 和 s11ch_sqlncli.chm）将安装到以下位置：  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序的所有相应注册表设置都将在安装过程中完成。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 头文件和库文件（sqlncli.h 和 sqlncli11.lib）安装在以下位置：  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 除了安装之外[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 作为的一部分[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装，此外还有一个名为 sqlncli.msi 可以找到的可再发行组件安装程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装磁盘的以下位置：`%CD%\Setup\`.  
  
 您可以通过 sqlncli.msi 分发 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 在您部署某一应用程序时，可能需要安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 安装多个包（对于用户而言就像是一次安装）的一种方法就是使用链接器和引导程序技术。 有关详细信息，请参阅[为 Visual Studio 2005 创作自定义引导程序包](http://go.microsoft.com/fwlink/?LinkId=115667)和[添加自定义系统必备](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
 sqlncli.msi 的 x64 和 Itanium 版本也会安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的 32 位版。 如果您的应用程序所针对的目标平台并非其开发时所使用的平台，则可以从 Microsoft 下载中心下载针对 x64、Itanium 和 x86 的 sqlncli.msi 版本。  
  
 在调用 sqlncli.msi 时，默认情况下只会安装客户端组件。 这些客户端组件即为那些支持运行使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 开发的应用程序的文件。 若还要安装 SDK 组件，请在命令行中指定 `ADDLOCAL=All`。 例如：  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>无提示安装  
 如果您将 /passive、/qn、/qb 或 /qr 选项与 msiexec 一起使用，则必须还指定 IACCEPTSQLNCLILICENSETERMS=YES，以便显式指示您接受最终用户许可协议条款。 必须以全大写字母指定此选项。  
  
## <a name="uninstalling-sql-server-native-client"></a>卸载 SQL Server Native Client  
 因为应用程序，如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务器和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]工具依赖于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端，它是才能卸载[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前会卸载所有的从属应用程序，本机客户端。 向用户提供一条警告，你的应用程序依赖于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端，使用 APPGUID 安装选项在 MSI 中，如下所示：  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 传递给 APPGUID 的值是您的特定产品代码。 当使用 Microsoft Installer 捆绑应用程序安装程序时，必须创建产品代码。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Native Client 生成应用程序](installing-sql-server-native-client.md)   
 [安装操作指南主题](../../../sql-server/install/installation-how-to-topics.md)  
  
  
