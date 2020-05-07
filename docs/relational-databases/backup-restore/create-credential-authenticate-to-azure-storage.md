---
title: 创建凭据 - 向 Azure 存储进行身份验证 | Microsoft Docs
description: 在 SQL Server 中，使用“备份数据库”对话框的“创建凭据”页可提供 Azure 管理证书以验证连接。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 40ee955b5f8cc683d2ec4f875c688f5575a0a44a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82179221"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>创建凭据 - 向 Azure 存储进行身份验证
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用“备份到 URL - 创建凭据”对话框可创建新的 SQL 凭据  。  
  
 使用此对话框创建凭据时，必须提供一个添加到本地证书存储的 Azure 管理证书，或一个已下载到计算机的发布配置文件，以验证订阅和存储帐户信息。  
  
 **SQL 凭据**  
 指定要使用的 SQL 凭据的名称。  
  
## <a name="azure-credentials"></a>Azure 凭据  
 **管理证书**  
 可使用此选项从本地证书存储指定与 Azure 管理证书匹配的证书。 有关 Azure 管理证书的详细信息，请参阅[创建并上载 Azure 的管理证书](https://go.microsoft.com/fwlink/?LinkId=320781)。  
  
 **订阅**  
 选择、键入或粘贴与本地证书存储中的管理证书匹配的 Azure 订阅 ID。  
  
 **发布配置文件**  
 如果您有下载到计算机的发布配置文件，则可以使用此选项。 如果您使用此选项，则订阅 ID 和证书将自动填充。  
  
> [!CAUTION]  
>  SQL Server 当前支持发布配置文件版本 2.0。 要下载支持的发布配置文件版本，请参阅 [下载发布配置文件 2.0](https://go.microsoft.com/fwlink/?LinkId=396421)。  
  
## <a name="storage-account"></a>存储帐户  
 选择要用于存储备份文件的存储帐户。  
  
  
