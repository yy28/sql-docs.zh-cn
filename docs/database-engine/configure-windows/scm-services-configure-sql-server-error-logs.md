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
ms.openlocfilehash: 8e746861ef30305a901c388f7574a4a27e2edab4
ms.sourcegitcommit: 02b7fa5fa5029068004c0f7cb1abe311855c2254
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74127479"
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

      指定错误日志文件回收前创建的最大存档错误日志文件数。 默认值为 6，不包括当前文件。 该值决定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在回收备份日志前保留的以前的备份日志的数量。

    B. 日志文件大小

      **错误日志文件的大小上限（以 KB 为单位）**

      可以设置每个文件的大小量（以 KB 为单位）。 如果将它保留为 0，则日志大小不受限制。
