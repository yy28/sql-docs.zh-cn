---
title: "创建凭据 - 向 Azure 存储进行身份验证 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f4cc42e5233c3e58bde7cac1713e6da28a0e573
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-credential---authenticate-to-azure-storage"></a>创建凭据 - 向 Azure 存储进行身份验证
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用“备份到 URL - 创建凭据”对话框可创建新的 SQL 凭据。  
  
 使用此对话框创建凭据时，必须提供一个添加到本地证书存储的 Windows Azure 管理证书，或一个已下载到计算机的发布配置文件，以验证订阅和存储帐户信息。  
  
 **SQL 凭据**  
 指定要使用的 SQL 凭据的名称。  
  
## <a name="windows-azure-credentials"></a>Windows Azure 凭据  
 **管理证书**  
 可使用此选项从本地证书存储指定与 Windows Azure 管理证书匹配的证书。 有关 Windows Azure 管理证书的详细信息，请参阅 [创建并上载 Windows Azure 的管理证书](http://go.microsoft.com/fwlink/?LinkId=320781)。  
  
 **订阅**  
 选择、键入或粘贴与本地证书存储区中的管理证书匹配的 Windows Azure 订阅 ID。  
  
 **发布配置文件**  
 如果您有下载到计算机的发布配置文件，则可以使用此选项。 如果您使用此选项，则订阅 ID 和证书将自动填充。  
  
> [!CAUTION]  
>  SQL Server 当前支持发布配置文件版本 2.0。 要下载支持的发布配置文件版本，请参阅 [下载发布配置文件 2.0](http://go.microsoft.com/fwlink/?LinkId=396421)。  
  
## <a name="storage-account"></a>存储帐户  
 选择要用于存储备份文件的存储帐户。  
  
  
