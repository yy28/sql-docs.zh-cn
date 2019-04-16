---
title: 无法升级只读数据库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3f751f4058d29c6ce27a5a1d608f3fb076cc300
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583250"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>无法升级只读数据库
  升级顾问已确定此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的某些数据库无法升级。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 已检测到一个只读数据库。 若要升级此数据库，安装程序必须能写入此数据库。  
  
## <a name="corrective-action"></a>纠正措施  
 当没有人使用该数据库时，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]企业管理器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，或要更改为读写的数据库的 ALTER DATABASE 语句。 下面的语句可将数据库更改为可读写状态。  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 有关 ALTER DATABASE 语句的详细信息，请参阅 [!INCLUDE[tsql](../../includes/tsql-md.md)] 联机丛书中的“ALTER DATABASE ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])”主题。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
