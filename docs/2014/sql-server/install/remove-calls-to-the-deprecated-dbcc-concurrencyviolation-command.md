---
title: 删除对不推荐使用 DBCC CONCURRENCYVIOLATION 命令的调用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2486546efae7daa63441e12fa350ef878c7daa77
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261893"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>删除对不推荐使用的 DBCC CONCURRENCYVIOLATION 命令的调用
  升级顾问检测到使用了 DBCC CONCURRENCYVIOLATION 命令。 此命令不再可用。 执行此命令返回错误 2526。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有任何最近版本包括工作负荷调控器；因此该命令已被删除。  
  
## <a name="corrective-action"></a>纠正措施  
 更新应用程序和脚本以删除对这一不推荐使用的命令的引用。  
  
## <a name="external-resources"></a>外部资源  
  
