---
title: 创建凭据 - 向 Azure 存储进行身份验证 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2c5428611c67315407ed31478fbb60ccca1b6dd2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351344"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>创建凭据 - 向 Azure 存储进行身份验证
  使用“备份到 URL - 创建凭据”对话框可创建新的 SQL 凭据。  
  
 使用此对话框创建凭据时，必须提供一个添加到本地证书存储的 Windows Azure 管理证书，或一个已下载到计算机的发布配置文件，以验证订阅和存储帐户信息。  
  
 **SQL 凭据**  
 指定要使用的 SQL 凭据的名称。  
  
## <a name="windows-azure-credentials"></a>Windows Azure 凭据  
 **管理证书**  
 可使用此选项从本地证书存储指定与 Windows Azure 管理证书匹配的证书。 有关 Windows Azure 管理证书的详细信息，请参阅 [创建并上载 Windows Azure 的管理证书](https://go.microsoft.com/fwlink/?LinkId=320781)。  
  
 **订阅**  
 选择、键入或粘贴与本地证书存储区中的管理证书匹配的 Windows Azure 订阅 ID。  
  
 **发布配置文件**  
 如果您有下载到计算机的发布配置文件，则可以使用此选项。 如果您使用此选项，则订阅 ID 和证书将自动填充。  
  
> [!CAUTION]  
>  SQL Server 当前支持发布配置文件版本 2.0。 要下载支持的发布配置文件版本，请参阅 [下载发布配置文件 2.0](https://go.microsoft.com/fwlink/?LinkId=396421)。  
  
## <a name="storage-account"></a>存储帐户  
 选择要用于存储备份文件的存储帐户。  
  
  
