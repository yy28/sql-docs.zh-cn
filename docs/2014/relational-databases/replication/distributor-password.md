---
title: 分发服务器密码 | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6d3c7971f6d5e117ae923ee8697a4ec51e1a34e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721467"
---
# <a name="distributor-password"></a>分发服务器密码
  在此向导的 **“发布服务器”** 页上，如果允许一个或多个发布服务器将此服务器作为远程分发服务器，则必须为复制使用 **distributor_admin** 登录名在发布服务器和远程分发服务器之间建立的连接指定密码。 在新建发布向导或配置分发向导的 **“管理密码”** 页上，必须为每个使用此远程分发服务器的发布服务器输入相同的密码。 有关分发服务器的安全性的详细信息，请参阅[保护分发服务器](security/secure-the-distributor.md)。  
  
## <a name="options"></a>选项  
 **密码**  
 为发布服务器和远程分发服务器之间的连接输入强密码。  
  
 **确认密码**  
 重新输入密码以确认密码输入正确。  
  
## <a name="see-also"></a>另请参阅  
 [“配置分发”](configure-distribution.md)   
 [配置发布和分发](configure-publishing-and-distribution.md)  
  
  
