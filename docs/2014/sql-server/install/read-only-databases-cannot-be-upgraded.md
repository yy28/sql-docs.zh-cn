---
title: 只读数据库无法升级 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ba48ed2bd80961a4949dc13f04fed0637ecc27ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054680"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>无法升级只读数据库
  升级顾问已确定此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的某些数据库无法升级。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 已检测到一个只读数据库。 若要升级此数据库，安装程序必须能写入此数据库。  
  
## <a name="corrective-action"></a>纠正措施  
 如果没有人在使用数据库，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 企业管理器、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 ALTER database 语句将数据库更改为读写数据库。 下面的语句可将数据库更改为可读写状态。  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 有关 ALTER DATABASE 语句的详细信息，请参阅 [!INCLUDE[tsql](../../includes/tsql-md.md)] 联机丛书中的“ALTER DATABASE ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])”主题。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
