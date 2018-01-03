---
title: "SQL Server Migration Assistant 用于访问 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/14/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: 0afeb32a33ee09789c08785fe49d38dd1a783c65
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>访问 (AccessToSQL) 的 SQL Server 迁移助手
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 的访问是一个用于迁移工具从数据库[!INCLUDE[msCoName](../../includes/msconame_md.md)]访问到 2010 年 97 版本[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Windows 和 Linux （预览版） 上的自 2017 年 1 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL DB。 访问的 SSMA 将转换到的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库对象，加载到这些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL，然后将数据迁移到的访问从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL。  
  
本文档向您介绍 SSMA for Access，并提供有关访问数据库迁移到的分步说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 以及有关在迁移后可能发生的问题的信息。  
  
## <a name="contents"></a>目录  
  
|部分|Description|  
|-----------|---------------|  
|[SSMA for Access 中的新增功能](http://msdn.microsoft.com/en-us/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出对 SSMA 版本的更改。|  
|[安装访问的 SQL Server 迁移的助手](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|列出安装 SSMA，安装和许可 SSMA，以及指向最新版本的过程的先决条件。|  
|[开始使用 SQL Server Migration Assistant 获得访问 &#40;AccessToSQL &#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|介绍 SSMA 和其用户界面。|  
|[为迁移准备的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|描述如何准备好转换为 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure。|  
|[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)|提供转换过程和过程中每个步骤的详细的信息的概述。|  
|[链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)|介绍如何使用现有的 Access 应用程序，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[用户界面参考](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)|包含 SSMA 对话框中的文档。|  
|[使用 SSMA for Access 控制台](http://msdn.microsoft.com/en-us/ef94e843-9f88-45a2-86c4-a0af268738c4)|包含有关 SSMA 控制台应用程序的文档|  
|[获取用于访问的 SSMA 帮助](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助信息。|  
  
