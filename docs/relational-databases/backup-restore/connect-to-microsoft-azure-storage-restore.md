---
title: 连接到 Microsoft Azure 存储（还原）| Microsoft Docs
description: 在 SQL Server 中，通过“Azure 存储帐户”对话框可以指定与 Azure 存储帐户信息的连接，以便获取 Azure 帐户中的文件存储。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7c6564d9dc63a4d2e35ac306db91cead15f024c6
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220452"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>连接到 Microsoft Azure 存储（还原）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可使用该对话框来指定与 Azure 存储帐户信息的连接，以便检索 Azure 存储帐户中的文件存储。 在指定所需信息后，请单击“连接”  以与 Azure 存储建立连接。  
  
## <a name="azure-storage-account"></a>Azure 存储帐户  
 **存储帐户**  
 选择、键入或粘贴要使用的 Azure 存储帐户名称。 下拉框会列出以前使用的帐户。  
  
 **帐户密钥**  
 指定 Azure 存储帐户访问密钥。  
  
 **使用安全端点 (HTTPS)** 复选框  
 选择此选项可与 Azure 存储建立安全连接（建议使用）。  
  
 **保存帐户密钥** 复选框  
 如果希望 SQL Server 记住此存储帐户的访问密钥，请选中此复选框。  
  
### <a name="sql-credential"></a>SQL 凭据  
 **选择现有凭据**  
 选择与存储帐户和帐户密钥信息匹配的现有 SQL 凭据。  
  
 **创建新凭据**  
 选择此选项可使用存储帐户和帐户密钥信息创建新的凭据。 在 **“凭据名称”** 字段中指定新凭据的名称。  
  
  
