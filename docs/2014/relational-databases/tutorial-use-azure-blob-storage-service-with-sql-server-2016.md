---
title: 教程：在 Azure 存储服务中 SQL Server 数据文件 |Microsoft Docs
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
ms.openlocfilehash: a15f6735ef0ef79b7eb953445c926f60f6bfb12e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176083"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>教程：Azure 存储服务中的 SQL Server 数据文件
  欢迎使用 Azure 存储服务中的 SQL Server 数据文件教程。 本教程有助于了解如何将 SQL Server 数据文件直接存储在 Azure Blob 存储服务中。  
  
 Azure Blob 存储服务 SQL Server 集成支持是一种 SQL Server 2014 增强。 有关使用此功能的功能和优势的概述，请参阅[SQL Server Azure 中的数据文件](databases/sql-server-data-files-in-microsoft-azure.md)。  
  
## <a name="what-you-will-learn"></a>要学习的知识  
 本教程介绍了如何在 Azure 存储服务中将 SQL Server 的数据文件存储在多个课程中。 每一课都以一个特定任务为重点。 首先，你将学习如何在 Azure 中创建存储帐户和容器。 然后，你将了解如何创建 SQL Server 凭据，以便能够将 SQL Server 与 Azure 存储集成。 然后，将直接在 Azure 存储中创建数据库。 另外，此教程还将演示加密、迁移以及备份和还原方案。  
  
 本教程分为 9 课：  
  
 **[第 1 课：创建 Azure 存储帐户和容器](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 在本课程中，将创建 Azure 存储帐户和容器。  
  
 **[第2课。在容器上创建策略并生成共享访问签名 &#40;SAS&#41; 密钥](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 在本课中，您将在 Blob 容器上创建策略并生成共享访问签名。  
  
 **[第 3 课：创建 SQL Server 凭据](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 在本课中，你将创建凭据，以存储用于访问 Azure 存储帐户的安全信息。  
  
 **[第 4 课：在 Azure 存储中创建数据库](../relational-databases/lesson-3-database-backup-to-url.md)**  
 在本课程中，将使用 "创建数据库文件名" 选项在 Azure 存储中创建数据库。  
  
 **[第5课。&#40;可选&#41; 使用 TDE 加密数据库](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 在本课中，您将使用透明数据加密 (TDE) 和服务器证书对数据库进行加密。  
  
 **[第 6 课：将数据库从本地源计算机迁移至 Azure 中的目标计算机](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 本课程介绍如何使用 CREATE DATABASE FOR ATTACH 将数据库从本地迁移到 Azure 中的虚拟机。  
  
 **[第 7 课：将数据文件移动到 Azure 存储](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 在本课中，将使用 ALTER DATABASE 语句将数据文件移到 Azure 存储。  
  
 **[第8课。将数据库还原到 Azure 存储](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 在本课中，您将使用 RESTORE Database MOVE 选项将数据库还原到 Azure 存储。  
  
 **[第9课：从 Azure 存储还原数据库](lesson-8-restore-as-new-database-from-log-backup.md)**  
 在本课中，您将使用 RESTORE Database MOVE 选项从 Azure 存储还原数据库。  
  
## <a name="see-also"></a>另请参阅  
 [Azure 中的 SQL Server 数据文件](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
