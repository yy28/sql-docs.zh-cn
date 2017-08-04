---
title: "SQL Server Migration Assistant 用于访问 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eabbda81defc597d99b82a928a1ca69baedb6328
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>访问 (AccessToSQL) 的 SQL Server 迁移助手
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 的访问是一个用于迁移工具从数据库[!INCLUDE[msCoName](../../includes/msconame_md.md)]访问到 2010 年 97 版本[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] SQL Azure。 访问的 SSMA 将转换到的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库对象，加载这些对象到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然后再将数据迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
本文档向你介绍 SSMA for Access，提供有关访问数据库迁移到的分步说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，并提供有关在迁移后可能出现的问题的信息。  
  
## <a name="contents"></a>目录  
  
|部分|Description|  
|-----------|---------------|  
|[什么是 SSMA for Access 中的新增功能](http://msdn.microsoft.com/en-us/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出对 SSMA 版本的更改。|  
|[安装访问的 SQL Server 迁移的助手](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|列出安装 SSMA，安装和许可 SSMA，以及指向最新版本的过程的先决条件。|  
|[开始使用 SQL Server Migration Assistant 获得访问 &#40;AccessToSQL &#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|介绍 SSMA 和其用户界面。|  
|[为迁移准备的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|描述如何准备好转换为 Access 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure。|  
|[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)|提供转换过程和过程中每个步骤的详细的信息的概述。|  
|[链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)|介绍如何使用现有的 Access 应用程序，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[用户界面参考](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)|包含 SSMA 对话框中的文档。|  
|[为访问控制台使用 SSMA](http://msdn.microsoft.com/en-us/ef94e843-9f88-45a2-86c4-a0af268738c4)|包含有关 SSMA 控制台应用程序的文档|  
|[获取用于访问的 SSMA 帮助](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助信息。|  
  

