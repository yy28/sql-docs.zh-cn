---
title: SQL Server 代理属性（“登录”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 01fc6329-5d6b-4186-9565-395f375477bb
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a5cfc683639e418a6fab6720fe3aa5b00f6e5767
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015368"
---
# <a name="sql-server-agent-properties-log-on-tab"></a>SQL Server 代理属性（“登录”选项卡）
  使用 **“SQL Server 代理属性”** 对话框中的 **“登录”** 选项卡，可以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务使用的帐户，还可以启动和停止该服务。 对帐户密码的更改立即生效，无需重新启动服务。  
  
> [!NOTE]  
>  更改群集实例的服务使用的帐户名时，新帐户必须是安装期间为待更改服务指定的域组的成员，或者您必须具有向该组添加成员的权限。 如果您无权修改组成员身份，请与域管理员联系。  
  
## <a name="options"></a>“常规”  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的信息，请在联机丛书中搜索“设置 Windows 服务帐户”。  
  
 **帐户名**  
 指定本地用户帐户名或域用户帐户名。  
  
 **密码**  
 键入帐户的密码。  
  
 **确认密码**  
 再次键入帐户的密码。  
  
 **开始**  
 启动服务。  
  
 **停止**  
 停止服务。  
  
 **暂停**  
 暂停服务。  
  
 **恢复**  
 恢复暂停的服务。  
  
  