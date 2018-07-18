---
title: Access (AccessToSQL) 的 SQL Server 迁移助手 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/14/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 3ffc062101434178ba5739c553508202d6b73c6a
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985599"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>Access (AccessToSQL) 的 SQL Server 迁移助手
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 迁移助手 (SSMA) for Access 是一个工具，用于迁移数据库从[!INCLUDE[msCoName](../../includes/msconame_md.md)]访问到版本 97 到 2010年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 在 Windows 和 Linux （预览版） 上的 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL DB。 适用于 Access 的 SSMA 将转换到访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 数据库对象，这些对象合并的负载[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL，然后再将数据迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL。  
  
本文档向您介绍 SSMA for Access，并提供了分步说明 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 以及迁移后可能出现的问题有关的信息。  
  
## <a name="contents"></a>目录  
  
|部分|Description|  
|-----------|---------------|  
|[SSMA for Access 中的新增功能](http://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出了对 SSMA 版本的更改。|  
|[安装用于访问 SQL Server 迁移助手](http://msdn.microsoft.com/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|列出了安装 SSMA，用于安装和许可 SSMA，以及指向最新版本的过程的先决条件。|  
|[开始使用用于访问 SQL Server 迁移助手&#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|引入了 SSMA 和其用户界面。|  
|[为迁移准备 Access 数据库](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|介绍如何准备您的 Access 数据库转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure。|  
|[Access 数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)|提供有关在过程中每个步骤的详细的信息的转换过程的概述。|  
|[链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)|介绍如何使用现有的 Access 应用程序，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[用户界面参考](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)|包含文档 SSMA 对话框。|  
|[使用 SSMA for Access 控制台](http://msdn.microsoft.com/ef94e843-9f88-45a2-86c4-a0af268738c4)|包含有关 SSMA 控制台应用程序的文档|  
|[获取 SSMA 帮助进行访问](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助信息。|  
  
