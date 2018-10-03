---
title: SQL Server 复制 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f3c9b4734dd77424805815eafca29380b17caf8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049688"
---
# <a name="sql-server-replication"></a>SQL Server 复制
  复制是一组技术，它将数据和数据库对象从一个数据库复制和分发到另一个数据库，然后在数据库之间进行同步以保持一致性。 使用复制，可以在局域网和广域网、拨号连接、无线连接和 Internet 上将数据分发到不同位置以及分发给远程或移动用户。  
  
 事务复制通常用于需要高吞吐量的服务器到服务器方案（包括：提高可伸缩性和可用性、数据仓库和报告、集成多个站点的数据、集成异类数据以及减轻批处理的负荷）。 合并复制主要是为可能存在数据冲突的移动应用程序或分步式服务器应用程序设计的。 常见应用场景包括：与移动用户交换数据、POS（消费者销售点）应用程序以及集成来自多个站点的数据。 快照复制用于为事务复制和合并复制提供初始数据集；在适合数据完全刷新时也可以使用快照复制。 利用这三种复制， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供功能强大且灵活的系统，以便使企业范围的数据同步。 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 和 [!INCLUDE[win8](../../includes/win8-md.md)]都支持复制到 SQLCE 3.5 和 SQLCE 4.0。  
  
 除了复制以外，还可以使用 Microsoft Sync Framework 来同步数据库。 Sync Framework 提供了相关的组件和一个直观且灵活的 API，使得在 SQL Server、SQL Server Express、SQL Server Compact 和 SQL Azure 数据库之间进行同步变得非常轻松。 Sync Framework 还包括一些类，它们可改写为在 SQL Server 数据库和任何其他与 ADO.NET 兼容的数据库之间进行同步。 有关 Sync Framework 数据库同步组件的详细文档，请参阅 [同步数据库](http://go.microsoft.com/fwlink/?LinkId=209079)。 有关 Sync Framework 的概述，请参阅 [Microsoft Sync Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=209078)。 有关 Sync Framework 与合并复制的比较，请参阅 [同步数据库概述](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **按区域浏览内容**  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")[新增功能](what-s-new-replication.md)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")[向后兼容性](replication-backward-compatibility.md)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")[复制功能和任务](replication-features-and-tasks.md)  
  
 ![小文件文件夹图标](../../integration-services/media/filefolder-small.gif "小文件文件夹图标")[技术参考](technical-reference-replication.md)  
  
  
