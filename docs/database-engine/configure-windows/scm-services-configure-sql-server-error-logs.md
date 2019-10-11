---
title: 配置 SQL Server 错误日志 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21737a329fdd6bf68f1bf7df5f4df4511b26cfd9
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688325"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM 服务 - 配置 SQL Server 错误日志

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何查看或修改回收 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志的方式。  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>打开“配置 SQL Server 错误日志”对话框  

1. 在对象资源管理器中，展开 SQL Server 的实例，展开  “管理”，右键单击  “SQL Server 日志”，再单击  “配置”。

2. 在 **“配置 SQL Server 错误日志”** 对话框中，从以下选项中进行选择。

    A. 日志文件计数

      **限制错误日志文件在回收之前的数目**

      若选中此选项，将限制在错误日志回收前可以创建的错误日志数。 每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时都将创建新的错误日志。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将保留前六个日志的备份，除非选中此选项并在下面指定一个不同的最大错误日志文件数。  
  
      **最大错误日志文件数**

      指定错误日志文件回收前创建的最大错误日志文件数。 默认值为 6，表示 1 个当前备份日志和 5 个之前的备份日志，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在回收之前将一直保留这些日志。

    B. 日志文件大小

      **错误日志文件的大小上限（以 KB 为单位）**

      可以设置每个文件的大小量（以 KB 为单位）。 如果将它保留为 0，则日志大小不受限制。
