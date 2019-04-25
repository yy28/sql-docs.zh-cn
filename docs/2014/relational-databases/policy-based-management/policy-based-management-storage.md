---
title: 基于策略的管理存储 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e1eab3ad745a83a8a55545570e020c1f1af732ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628873"
---
# <a name="policy-based-management-storage"></a>基于策略的管理存储
  策略存储在 msdb 数据库中。 在更改策略或条件后，应对 msdb 进行备份。 有关详细信息，请参阅[备份和还原系统数据库 (SQL Server)](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
## <a name="storing-policies"></a>存储策略  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包括可用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的策略。 默认情况下，这些策略不安装在上[!INCLUDE[ssDE](../../includes/ssde-md.md)]; 但是，可以从默认安装位置 C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 的要导入。  
  
 可以使用“文件/新建”菜单直接创建策略，然后将这些策略保存到文件中。 这样，在未连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的情况下也可以创建策略。  
  
 在当前 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中评估的策略的策略历史记录保存在 msdb 系统表中。 不会保留应用于 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的其他实例、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的策略的策略历史记录。  
  
  
