---
title: Web 服务器信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c40a9e43e15e948f816379ee751de7ad529a67dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127062"
---
# <a name="web-server-information"></a>Web 服务器信息
  若要使用合并复制的 Web 同步选项，必须提供 Web 服务器信息。 有关配置 Web 同步的信息，请参阅[配置 Web 同步](configure-web-synchronization.md)。  
  
## <a name="options"></a>“常规”  
 **Web 服务器地址**  
 如果在“发布属性”对话框的“FTP 快照和 Internet”页中指定了 Web 服务器地址，该地址将作为默认值显示在此文本框中。 您可以接受此默认值，也可以为同步此订阅的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet 信息服务 (IIS) 服务器输入完全限定的 Web 服务器地址。  
  
 **各个订阅服务器将如何连接到 Web 服务器?**  
 指定用于连接到 Web 服务器的身份验证的类型。 建议您将基本身份验证与安全套接字层 (SSL) 一起使用，以连接到 IIS 服务器。 如果选择了基本身份验证，请输入用于从订阅服务器连接到 IIS 服务器的登录名和密码。  
  
## <a name="see-also"></a>请参阅  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [查看和修改请求订阅属性](view-and-modify-pull-subscription-properties.md)   
 [非 SQL Server 订阅服务器](non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [合并复制的 Web 同步](web-synchronization-for-merge-replication.md)  
  
  