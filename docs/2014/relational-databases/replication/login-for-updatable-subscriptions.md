---
title: 可更新订阅的登录名 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8162c7654d99cd2ebab41d290c0a39c6c686686
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135367"
---
# <a name="login-for-updatable-subscriptions"></a>可更新订阅的登录名
  如果在此向导的 **“可更新订阅”** 页上选择 **“复制”** ，则必须在与发布服务器建立连接的订阅服务器上指定一个帐户以立即更新订阅。 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 即使在 **“可更新订阅”** 页上选择 **“对更改进行排队并在可能时提交”** ，也需要使用此帐户，因为默认情况下，新建订阅向导将排队更新配置为在必要时可切换到立即更新。  
  
> [!IMPORTANT]  
>  对于指定的连接帐户，只能授予对复制功能在发布数据库中创建的视图插入、更新和删除数据的权限，而不应授予任何其他权限。 对于发布数据库中的视图（名称格式为 **syncobj_**_\<HexadecimalNumber>_），请将其权限授予在每个订阅服务器上配置的帐户。  
  
 有三种连接类型可以选择：  
  
-   已定义的链接服务器或远程服务器。  
  
-   复制创建的链接服务器；用在此向导中指定的凭据建立连接。  
  
-   复制创建的链接服务器；用在订阅服务器上做更改的用户的凭据建立连接。  
  
 可以在此向导中指定前两个选项。 最后一个选项只能使用 [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 指定；将参数 **@security_mode** 的值指定为 **1**。  
  
## <a name="options"></a>选项  
 **创建使用以下 SQL Server 身份验证登录名进行连接的链接服务器：**  
 复制使用在 **“登录名”** 和 **“密码”** 字段中指定的凭据创建链接服务器。  
  
 **“登录名”**  
 输入仅具有本主题中所描述权限的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 **“密码”**  
 为 **“登录名”** 中指定的登录名输入一个强密码。  
  
 **确认密码**  
 重新输入密码以确认密码输入正确。  
  
 **使用您指定的链接服务器或远程服务器。**  
 此选项需要使用您所定义的链接服务器或远程服务器。 有关详细信息，请参阅[链接服务器（数据库引擎）](../linked-servers/linked-servers-database-engine.md)和[远程服务器](../../database-engine/configure-windows/remote-servers.md)。 请确保用于链接服务器或远程服务器的登录名具有强密码，并且仅具有本主题中描述的权限。  
  
## <a name="see-also"></a>请参阅  
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [查看和修改复制安全设置](security/view-and-modify-replication-security-settings.md)   
 [事务发布的可更新订阅](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
