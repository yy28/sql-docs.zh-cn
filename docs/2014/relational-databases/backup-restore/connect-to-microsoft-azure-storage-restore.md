---
title: 连接到 Azure 存储（还原） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb4a8943c237e37ca612bf367abe99d47c8eb08
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958782"
---
# <a name="connect-to-azure-storage-restore"></a>连接到 Azure 存储（还原）
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
  
  
