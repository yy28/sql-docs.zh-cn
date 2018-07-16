---
title: 确定是否已安装并启动数据库引擎 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 619fbc9818e627d58a018723475f6f97493df49b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265363"
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>确定是否已安装并启动数据库引擎
  成功安装 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 后可将文件安装到文件系统，在注册表中创建注册表项并安装数个工具。 本主题说明如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置管理器来确定是否已在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中安装并启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>如何使用 SQL Server 配置管理器查看和启动数据库引擎  
  
1.  单击 **“开始”**，依次指向 **“所有程序”**、 **Microsoft SQL Server**、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
     如果在 **“开始”** 菜单中没有这些项，则不能正确安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 运行安装程序以安装 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。  
  
2.  在 **SQL Server 配置管理器**的左窗格中，单击 **“SQL Server 服务”**。 此时右窗格列出多项与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相关的服务。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 已安装，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务将作为 **SQL Server (MSSQLSERVER)** 列出（如果它是默认实例）；如果 **作为命名实例安装，则该服务将作为**\<*SQL Server (*>**instance_name**) [!INCLUDE[ssDE](../../includes/ssde-md.md)] 列出。 除非更改实例名称，否则将 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 安装为具有名称 **SQLEXPRESS**的命名实例。 绿色的三角形图标指示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在运行。 红色的正方形图标指示[!INCLUDE[ssDE](../../includes/ssde-md.md)]已停止。  
  
3.  若要启动[!INCLUDE[ssDE](../../includes/ssde-md.md)]，请在右窗格中，右键单击 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，再单击“启动”。  
  
> [!NOTE]  
>  安装过程中，用户可以选择安装程序文件和数据库文件的位置。 如果用户接受默认位置，文件将安装到 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] 和 C:\Program Files\Microsoft SQL Server\MSSQL.*x*，其中 *x* 为编号。  
  
  
