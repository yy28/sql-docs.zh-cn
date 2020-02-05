---
title: 使用数据库邮件而不是 SQL Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c029883591c49c1be52d23a025ff522b4095a6f5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68069156"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>使用数据库邮件而不是 SQL Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查 sys.configurations 目录视图以确定 SQL Mail XPs 服务器范围配置选项是否已设置为 ON。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的将来版本中将删除 SQL Mail。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 要发送邮件，请使用“数据库邮件”。  
  
 SQL Mail 在进程内运行到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 如果 SQL Mail 关闭，服务器也会关闭。 数据库邮件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外的单独进程内运行，它是可伸缩的，并且不需要在生产服务器上安装扩展 MAPI 客户端组件。  
  
## <a name="for-more-information"></a>有关详细信息  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
