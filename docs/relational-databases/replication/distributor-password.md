---
title: 分发服务器密码 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 53605b1e88c47c5fa9b2f0ee37147993e0375808
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "76283944"
---
# <a name="distributor-password"></a>分发服务器密码
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  在此向导的 **“发布服务器”** 页上，如果允许一个或多个发布服务器将此服务器作为远程分发服务器，则必须为复制使用 **distributor_admin** 登录名在发布服务器和远程分发服务器之间建立的连接指定密码。 在新建发布向导或配置分发向导的 **“管理密码”** 页上，必须为每个使用此远程分发服务器的发布服务器输入相同的密码。 有关分发服务器的安全性的详细信息，请参阅[保护分发服务器](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
## <a name="options"></a>选项  
 **密码**  
 为发布服务器和远程分发服务器之间的连接输入强密码。  
  
 **确认密码**  
 重新输入密码以确认密码输入正确。  
  
## <a name="see-also"></a>另请参阅  
 [“配置分发”](../../relational-databases/replication/configure-distribution.md)   
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
