---
title: 使用升级顾问来准备升级 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab9c51ba125a7489d693a1af6b16e432e8fb7099
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "73632738"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>使用升级顾问来准备升级
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级顾问可以帮助您做好升级至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的准备。 升级顾问分析早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已安装的组件，然后生成报告，指出在升级之前或之后应解决的问题。  
  
## <a name="how-upgrade-advisor-works"></a>升级顾问如何工作  
 运行升级顾问时，将显示“升级顾问”主页。 通过该主页，可以运行以下工具：  
  
-   升级顾问分析向导  
  
-   升级顾问报表查看器  
  
-   升级顾问帮助  
  
 第一次使用升级顾问时，应运行升级顾问分析向导来分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。 该向导完成分析后，请使用升级顾问报表查看器查看生成的报表。 每个报表中均有指向升级顾问帮助信息的链接，这些信息可帮助您修复已知问题或减少已知问题的影响。  
  
## <a name="upgrade-advisor-analysis"></a>升级顾问分析  
 升级顾问会对以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件进行分析：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 该分析会检查可以访问的对象，例如脚本、存储过程、触发器和跟踪文件。 升级顾问不能对桌面应用程序或加密的存储过程进行分析。  
  
 输出的格式为 XML 报表。 通过使用升级顾问报表查看器可查看 XML 报表。  
  
> [!NOTE]  
>  报表可能包含有“其他升级问题”项。 此项链接至一个问题列表，其中列出的问题是升级顾问未检测到但却可能存在于服务器或应用程序中的问题。 应查看无法检测的问题的列表，以确定是否由于这些无法检测的问题而必须更改服务器或应用程序。  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>如何安装和运行升级顾问  
 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级顾问的位置取决于您将分析的内容。 升级顾问支持对除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之外的所有受支持组件进行远程分析。 如果不扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的实例，则可在能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并满足升级顾问先决条件的任何计算机中安装升级顾问。 有关详细信息，请参阅 [支持的版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。 如果要扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例，则必须在报表服务器上安装升级顾问。  
  
 升级顾问在功能包中提供。  
  
 安装和运行升级顾问的前提条件如下：  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2、Windows 7 SP1 和 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1。  
  
-   Windows Installer（最低为 4.5 版）。 你可以从[Windows Installer](https://www.microsoft.com/download/details.aspx?id=8483)网站安装 Windows Installer。  
  
-   Microsoft .NET Framework 4。 在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]产品媒体上提供 .NET Framework 4，并从[.NET Framework 4 下载页](https://go.microsoft.com/fwlink/?LinkId=209895)获取。  
  
    -   若要从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 介质安装 .NET Framework 4，请找到磁盘驱动器的根目录。 然后双击 \redist 文件夹，再双击 DotNetFrameworks 文件夹，然后运行 dotNetFx40_Full_x86_x64.exe（对于 32 位操作系统或 64 位操作系统）。  
  
 若要通过 Web 安装升级顾问，请单击下载页上的下载按钮。 随后可以立即运行安装程序，也可以保存 SQLUA.msi 文件并稍后运行它。 如果要从产品光盘进行安装，请直接从产品磁盘中运行 SQLUA.MSI。  
  
 安装升级顾问之后，您可以从 "**开始**" 菜单中打开它：  
  
-   单击 "**开始**"，指向[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]"**所有程序**"，指向 ""，然后单击** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] "升级顾问**"。  
  
 有关详细信息，请参阅升级顾问下载和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 发行说明中包括的 Upgrade Advisor 文档。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server 的多个版本和实例](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [支持的版本和版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [向后兼容性](../../../2014/getting-started/backward-compatibility.md)  
  
  
