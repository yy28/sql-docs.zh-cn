---
title: "安装 SMO |Microsoft 文档"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bae4a59bc8365eae4bfcaba8610c1f3c11b8af97
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2017
---
#<a name="installing-smo"></a>安装 SMO

此页提供有关如何安装 SMO 使用应用程序和使用 SMO 的系统要求的信息。

## <a name="smo-nuget-package"></a>SMO NuGet 包

开头[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为分发 2017 SMO [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 包，以允许用户使用 SMO 开发应用程序。

这是 SharedManagementObjects.msi，以前作为 SQL Server 的每个版本的 SQL 功能包的一部分发布的替代。 使用 SMO 的应用程序应更新以改为使用 NuGet 包，并且将负责确保正在开发的应用程序安装二进制文件。

>>[!Important]
>>上所述[文件及其版本号](files-and-version-numbers.md)页上，不应 SMO 程序集安装到 GAC。 这样可能会导致问题的其他应用程序的也使用这些版本的 SMO (如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Studio)。

##<a name="installing-the-package"></a>安装包

请参阅[NuGet 快速入门-使用包](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package)有关说明和示例的安装和使用 NuGet 包。 
  
## <a name="system-requirements"></a>系统要求
  
 SMO 需要[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]4.0 若要运行，因此使用它的任何应用程序必须确保客户端计算机具有该版本或更高的版本。
  
