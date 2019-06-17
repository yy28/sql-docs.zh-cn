---
title: 教程：在 Windows Azure 存储服务的 SQL Server 数据文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e3d33209cd6dfe261a5deced345adac70b46961f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62523891"
---
# <a name="tutorial-sql-server-data-files-in-windows-azure-storage-service"></a>教程：Windows Azure 存储服务中的 SQL Server 数据文件
  欢迎使用“Windows Azure 存储服务中的 SQL Server 数据文件”教程。 本教程帮助您学习如何将 SQL Server 数据文件直接存储在 Windows Azure Blob 存储服务中。  
  
 Windows Azure Blob 存储服务的 SQL Server 集成支持是 SQL Server 2014 中的一项增强功能。 有关功能的概述和使用此功能的好处，请参阅[在 Windows Azure 中的 SQL Server 数据文件](databases/sql-server-data-files-in-microsoft-azure.md)。  
  
## <a name="what-you-will-learn"></a>学习内容  
 此教程通过多个课程说明如何将 SQL Server 数据文件存储在 Windows Azure 存储服务中。 每一课都以一个特定任务为重点。 首先，您将学习如何在 Windows Azure 中创建存储帐户和容器。 然后，您将学习如何创建 SQL Server 凭据，以便能够将 SQL Server 与 Windows Azure 存储集成。 接下来，您将直接在 Windows Azure 存储中创建数据库。 另外，此教程还将演示加密、迁移以及备份和还原方案。  
  
 本教程分为 9 课：  
  
 **[第 1 课：创建 Windows Azure 存储帐户和容器](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 在本课中，您将创建 Windows Azure 存储帐户和一个容器。  
  
 **[第 2 课。在容器上创建策略并生成共享访问签名&#40;SAS&#41;键](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 在本课中，您将在 Blob 容器上创建策略并生成共享访问签名。  
  
 **[第 3 课：创建 SQL Server 凭据](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 在本课中，您将创建凭据，以存储用于访问 Windows Azure 存储帐户的安全信息。  
  
 **[第 4 课：在 Windows Azure 存储中创建数据库](../relational-databases/lesson-3-database-backup-to-url.md)**  
 在本课中，您将使用 CREATE Database FILENAME 选项，在 Windows Azure 存储中创建数据库。  
  
 **[第 5 课。&#40;可选&#41;对使用 TDE 对数据库进行加密](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 在本课中，您将使用透明数据加密 (TDE) 和服务器证书对数据库进行加密。  
  
 **[第 6 课：将数据库从一个源计算机的本地到 Windows Azure 中的目标计算机](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 在本课中，您将使用 CREATE DATABASE FOR ATTACH 选项将数据库从本地迁移到 Windows Azure 中的虚拟机。  
  
 **[第 7 课：数据文件移到 Windows Azure 存储](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 在本课中，您将使用 ALTER DATABASE 语句将数据文件移至 Windows Azure 存储。  
  
 **[第 8 课：将数据库还原到 Windows Azure 存储](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 在本课程中，您将使用 RESTORE Database MOVE 选项将数据库还原到 Windows Azure 存储。  
  
 **[第 9 课。从 Windows Azure 存储还原数据库](lesson-8-restore-as-new-database-from-log-backup.md)**  
 在本课程中，您将使用 RESTORE Database MOVE 选项从 Windows Azure 存储还原数据库。  
  
## <a name="see-also"></a>请参阅  
 [Windows Azure 中的 SQL Server 数据文件](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
