---
title: "分析服务器属性 （选项卡上的日志） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a82e0c98-efaa-4b0b-9582-3c879ee42444
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5219e96dc9f0d198322aeb359ed608238a7fe84
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="analysis-server-properties-log-on-tab"></a>分析服务器属性（“登录”选项卡）
  使用 **“分析服务器属性”** 对话框中的 **“登录”** 选项卡可以指定 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 服务使用的帐户，还可以启动和停止该服务。  
  
> [!NOTE]  
>  更改群集实例上的服务使用的 **“帐户名”** 时，新帐户必须是安装期间为待更改服务指定的域组的成员，或者您必须有权添加该组的成员。 如果您无权修改组成员身份，请与域管理员联系。  
  
## <a name="options"></a>选项  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的信息，请在联机丛书中搜索主题“设置 Windows 服务帐户”。  
  
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
  
  
