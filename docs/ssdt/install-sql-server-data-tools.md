---
title: 安装 SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.package.stub
ms.assetid: 6f8616cb-9119-42c3-a9b1-936e088763e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a847748b0f0025402da1feb794f5c441ea2a3f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773565"
---
# <a name="install-sql-server-data-tools"></a>安装 SQL Server 数据工具
本主题介绍如何安装 SQL Server Data Tools。 SQL Server Data Tools 下载页（[ SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)）上提供了 SQL Server Data Tools 的更新。  
  
无论你使用的是 Visual Studio 2012 还是 Visual Studio 2013，请安装最新的 SQL Server Data Tools 更新以获取最新功能。  
  
## <a name="sql-server-data-tools-for-visual-studio-2013"></a>适用于 Visual Studio 2013 的 SQL Server Data Tools  
SQL Server Data Tools 包含在适用于 Web 的 Visual Studio 2013 Express、适用于桌面的 Visual Studio 2013 Express、Visual Studio Community 2013 以及包含 Professional SKU 和更高版本的所有付费 SKU 中。 在安装 Visual Studio 2013 后，你可以转到“工具”->“扩展和更新”->“更新”以了解是否有要安装的更新。  
  
## <a name="sql-server-data-tools-for-visual-studio-2012"></a>适用于 Visual Studio 2012 的 SQL Server Data Tools  
SQL Server Data Tools 在 Visual Studio 2012 中的 Professional SKU 或更高版本中提供。 安装 Visual Studio 2012 以及 SQL Server Data Tools 2012 年 11 月或更高版本的更新后，SQL Server Data Tools 可在有要安装的更新时进行报告。 有关详细信息，请参见[“检查更新”对话框](../ssdt/check-for-updates-dialog-box.md)。  
  
如果未安装 Visual Studio 2012，SQL Server Data Tools 将安装集成了 Shell 的 Visual Studio 2012 以及 SQL Server Data Tools。  
  
## <a name="administrative-installation-point"></a>管理安装点  
如果你需要在多个计算机或没有 Internet 访问权限的计算机上安装 SQL Server Data Tools ，则可以在网络共享或物理介质上创建一个管理安装布局，然后从该安装点进行安装。  
  
若要创建安装布局，请下载 SSDTSetup.EXE 并使用 `/layout`*位置* 选项运行它以在 *位置*处创建布局。 然后，用户可以从 *位置*运行 SSDTSetup.Exe。  
  
若要下载 SSDTSetup.exe，请转到 [安装最新的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)，单击你的 Visual Studio 版本对应的链接，然后下载你的语言对应的 SSDTSetup.exe。  
  
