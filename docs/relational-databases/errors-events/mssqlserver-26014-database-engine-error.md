---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a71f672ec2210c212e6e66221164224376ee4c89
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
  
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
  

