---
title: 安装 SQL Server 复制 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f63d8eee7708b70eedf9b9e00b85e646132dd986
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024383"
---
# <a name="install-sql-server-replication"></a>安装 SQL Server 复制
  可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导或通过命令提示符安装复制组件。 请在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或修改现有实例时安装复制组件。  
  
 安装复制组件后，必须配置服务器才可以使用复制。 有关详细信息，请参阅 [联机丛书中的](../../relational-databases/replication/configure-distribution.md) 配置分发 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!IMPORTANT]  
>  如果在修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的现有实例时安装复制组件，则在安装完成后必须停止并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。 此操作可帮助确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理能够识别复制代理子系统，并且可以在作业步骤中调用复制代理。  
  
## <a name="installing-replication-by-using-setup"></a>使用安装程序安装复制  
 **在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   若要安装包括复制管理对象 (RMO) 在内的复制组件，请在安装向导的“功能选择”页上选择“SQL Server 复制”。  
  
## <a name="installing-replication-from-the-command-prompt"></a>从命令提示符安装复制  
 **在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   请参阅[从命令提示符安装 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
## <a name="see-also"></a>请参阅  
 [安装 SQL Server 2014](install-sql-server.md)   
 [从命令提示符安装 SQL Server 2014](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  