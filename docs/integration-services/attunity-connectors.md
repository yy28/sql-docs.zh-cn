---
title: "Microsoft Connectors for Oracle 和 Teradata by Attunity (SSIS) |Microsoft 文档"
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors for Oracle 和 Teradata by Attunity for Integration Services (SSIS)

你可以在加载数据到或从 Oracle 或 Teradata SSIS 包中的时优化性能的 Integration services by Attunity 下载连接器。

## <a name="download-the-latest-attunity-connectors"></a>下载最新的 Attunity 连接器

获取此处的连接器的最新版本：  
[Microsoft Connectors for Oracle 和 Teradata 的 5.0 版](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>问题-Attunity 连接器不会显示在 SSIS 工具箱

若要查看 Attunity 连接器 SSIS 工具箱中的，始终需要安装目标版本的 SQL Server Data Tools (SSDT) 相同版本的 SQL Server 上安装了您的计算机的连接器的版本。 （您可能还必须安装的连接器的早期版本。）此要求是独立于你想要针对 SSIS 项目和包中的 SQL Server 版本。

例如，如果您已安装 SSDT 的最新版本，则使用生成号开头 14 必须版本 17 的 SSDT。 此版本的 SSDT 增加了对 SQL Server 2017 支持。 若要查看并使用 Attunity 中 SSIS 连接器打包开发-即使你想要面向 SQL Server 的早期版本-你还必须先安装 Attunity 连接器，版本 5.0 的最新版本。 此版本的连接器还增加了对 SQL Server 2017 支持。

检查从 Visual Studio 中的 SSDT 的已安装的版本**帮助** | **有关 Microsoft Visual Studio**，或在**程序和功能**控制面板中。 从下表，然后安装 Attunity 连接器的相应版本。

|SSDT 版本|SSDT 内部版本号|目标 SQL Server 版本|所需的版本的连接器|
|---------|---------|---------|---------|
|17|开头 14|SQL Server 2017|[Microsoft Connectors for Oracle 和 Teradata 的 5.0 版](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|开头 13|SQL Server 2016|[Microsoft Connectors for Oracle 和 Teradata 的 v4.0](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>下载最新 SQL Server Data Tools (SSDT)

获取最新版本的 SSDT 此处：  
[下载 SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
