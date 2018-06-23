---
title: 第 2 课： 评估按计划定期的最佳实践策略 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
caps.latest.revision: 4
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cd4874e722c12813eb574d94c073cc069f72a4b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124675"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>课程 2：定期评估最佳实践策略
  您可以对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一个或多个实例配置最佳实践策略的定期评估。 若要配置定义运行的最佳实践策略，您必须将这些策略导入到目标实例中。  
  
 若要将计划的策略部署到多个服务器中，您可以将这些策略导入到一个实例，为每个策略配置计划，将计划的策略导出到某一文件夹，然后通过已注册的服务器将计划的策略部署到目标实例。  
  
> [!IMPORTANT]  
>  目标实例必须运行 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或者更高版本。 自动过程要求在实例上本地存储策略，但早于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本不支持此功能。  
  
 在本课程中，您将执行以下操作：  
  
-   将最佳实践策略导入到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例中。  
  
-   配置要定期运行的策略。  
  
-   通过已注册的服务器将计划的最佳实践策略部署到多个实例。  
  
 本课程包含以下主题：  
  
-   [将策略导入到单个实例](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [计划策略](../../2014/tutorials/schedule-the-policies.md)  
  
-   [将计划的策略部署到多个实例](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>请参阅  
 [使用中央管理服务器管理多台服务器](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  