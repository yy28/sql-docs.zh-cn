---
title: 删除 SQL Server Data Tools 组件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f8ddb919-661f-4868-8c71-87c96f1f4487
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b114b99b816e10bc004cea8d60c56d296053c7c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685465"
---
# <a name="removing-sql-server-data-tools-components"></a>删除 SQL Server Data Tools 组件
在卸载 SSDT 或 Visual Studio 时，有些 SQL Server Data Tools (SSDT) 组件不会被删除。  
  
在卸载 SSDT 或 Visual Studio 时，计算机中不会删除以下 Windows 安装程序包 (.msi)。 删除这些组件会使 Visual Studio 的其他版本处于不受支持的状态。 如果您选择删除这些组件，请使用 Windows 的“添加或删除程序”：  
  
-   MicrosoftSQL Server Data Tools (SSDT.msi)  
  
-   MicrosoftSQL Server Data Tools Build Utilities (SSDTBuildUtilities.msi)  
  
-   SSDT 的必备组件 (SSDTDBSvcExternals.msi)  
  
在卸载 SSDT 之后，以下共享组件可能会由其他产品使用，并且将会留在计算机中。  
  
-   SQL Server 数据层应用程序框架 (DACFramework.msi)  
  
-   SQL Server 管理对象 (SharedManagementObjects.msi)  
  
-   SQL ServerTransact\-SQL 语言服务 (TSqlLanguageService.msi)  
  
-   MicrosoftSQL Server System CLR Types for SQL Server (SQLSysClrTypes.msi)  
  
-   SQL ServerTransact\-SQL ScriptDom (SQLDom.msi)  
  
-   SQL ServerTransact\-SQL 编译器服务 (SQLLs.msi)  
  
