---
title: 安装 SMO |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f57fc3ea1a677a2655f5358a1d5c4b27045ea6ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098021"
---
# <a name="installing-smo"></a>安装 SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

此页提供有关如何安装 SMO 使用应用程序和使用 SMO 的系统要求的信息。

## <a name="smo-nuget-package"></a>SMO NuGet 包

开头[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为分发 2017 SMO [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 包，以允许用户使用 SMO 开发应用程序。

这是 SharedManagementObjects.msi，以前为每个版本的 SQL Server 的 SQL 功能包的一部分发布的替换。 使用 SMO 的应用程序应更新，以改为使用 NuGet 包，并将负责确保二进制文件安装与正在开发的应用程序。

>>[!Important]
>>在所述[文件和版本号](files-and-version-numbers.md)页上，不应 SMO 程序集安装到 GAC 中。 执行此操作可能会与其他应用程序也使用这些版本的 SMO 造成问题 (如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Studio)。

## <a name="installing-the-package"></a>安装包

请参阅[NuGet 快速入门-使用包](https://docs.microsoft.com/nuget/quickstart/use-a-package)有关说明和示例的安装和使用 NuGet 包。 
  
## <a name="system-requirements"></a>系统要求
  
 SMO 需要[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]4.0 运行，因此使用它的任何应用程序必须确保客户端计算机具有该版本或更高版本。 一些本机二进制文件安装的 NetFx SMO 库还需要安装; VC 2013 运行时该运行时未包含在包中。 您可以下载 redist 适用于从目标体系结构 https://www.microsoft.com/download/details.aspx?id=40784
  
