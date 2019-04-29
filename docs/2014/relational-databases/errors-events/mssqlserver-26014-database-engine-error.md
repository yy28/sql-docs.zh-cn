---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edebfb36a1693f2a7d6a94d7c006d80e2bb27683
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914607"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|26014|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SNI_SSL_USER_CERT_FAILURE|  
|消息正文|无法加载用户指定的证书 [Cert Hash(sha1) "%hs"]。 服务器将不接受连接。 您应该验证是否正确安装了证书。 请参阅联机丛书中的“配置证书以供 SSL 使用”。|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试加载在该消息中指定的证书，但是该操作失败。 必须先解决此问题，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才能使用该证书。  
  
此错误可能的原因包括：  
  
-   该证书可能已被移动或删除。  
  
-   如果由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的登录名已发生更改，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能无权访问该证书。  
  
-   该证书可能已过期。  
  
## <a name="user-action"></a>用户操作  
请确保该消息中的命名证书在系统中存在，而且可供访问和使用。  
  
