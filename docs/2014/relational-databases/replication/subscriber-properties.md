---
title: 订阅服务器属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ad00d31b247dd606fcce39ea68ff60c5a0703216
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026303"
---
# <a name="subscriber-properties"></a>订阅服务器属性
  “订阅服务器属性”对话框包含与运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的订阅服务器有关的信息。  
  
## <a name="options"></a>“常规”  
 **到订阅服务器的代理连接**  
 分发代理和合并代理从分发服务器连接到订阅服务器时所处的上下文。此选项只适用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以前的版本。  
  
 选择 **“模拟代理进程帐户”** ，可以使用分发服务器上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理帐户的上下文连接到订阅服务器；也可以指定 **“SQL Server 身份验证”**，再输入 **“登录名”** 和 **“密码”** 的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您选择 **“模拟代理进程帐户”**。  
  
 对于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本，可以在新建订阅向导中为每个订阅指定连接信息，并可以在 **“订阅属性”** 对话框中更改连接信息。  
  
 **默认代理计划**  
 对于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]版本的订阅服务器，为新建订阅向导中所使用的默认计划。  
  
 **杂项**  
 包含有关订阅服务器和订阅服务器类型的信息。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   
 [属性参考（复制）](properties-reference-replication.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  