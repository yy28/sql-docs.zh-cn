---
title: 删除对不推荐使用 DBCC CONCURRENCYVIOLATION 命令的调用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 574b3de41498fa24d2cbd913899d4d071cca6053
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203547"
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
  
