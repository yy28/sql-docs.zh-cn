---
title: SQL Server Integration Services 属性（“登录”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0eb1b87-6bb0-475e-8492-0fd3c3f910ea
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2d46a9e86aaa261f32a0aab2c49891d8fc195a4e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129810"
---
# <a name="sql-server-integration-services-properties-log-on-tab"></a>SQL Server Integration Services 属性（“登录”选项卡）
  使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]“属性”对话框中的“登录”选项卡可指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务使用的帐户，并且可启动和停止该服务。  
  
## <a name="options"></a>“常规”  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的详细信息，请在联机丛书中搜索主题“设置 Windows 服务帐户”。  
  
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
  
  