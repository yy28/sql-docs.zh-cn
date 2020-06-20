---
title: 删除对不推荐使用的 DBCC CONCURRENCYVIOLATION 命令的调用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cde04ebfc2ea9996d1c9ed233123e5b66f6e81fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065213"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>删除对不推荐使用的 DBCC CONCURRENCYVIOLATION 命令的调用
  升级顾问检测到使用了 DBCC CONCURRENCYVIOLATION 命令。 此命令不再可用。 执行此命令返回错误 2526。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有任何最近版本包括工作负荷调控器；因此该命令已被删除。  
  
## <a name="corrective-action"></a>纠正措施  
 更新应用程序和脚本以删除对这一不推荐使用的命令的引用。  
  
## <a name="external-resources"></a>外部资源  
  
