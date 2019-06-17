---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c3b8e4690b0e0c501fee26648cd9632fdcf28b1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913683"
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|5554|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FS_MINIVER_OVERFLOW|  
|消息正文|单个文件的版本总数已达到文件系统所设置的最大限制。|  
  
## <a name="explanation"></a>解释  
 在多个活动的结果集 (MARS) 或触发器方案中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都使用由操作系统指定的最低版本。  
  
## <a name="user-action"></a>用户操作  
 尝试避免对同一事务中的数据进行重复更新。  
  
  
