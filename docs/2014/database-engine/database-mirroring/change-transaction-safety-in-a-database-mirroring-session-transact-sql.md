---
title: 更改数据库镜像会话中的事务安全 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d1d3fa972c60ae68c835a9e27da67d0ab970f372
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124627"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>更改数据库镜像会话中的事务安全 (Transact-SQL)
  事务安全是控制会话运行模式的属性。 但是，数据库所有者可以随时更改事务安全。 默认情况下，事务安全级别的设置为 FULL（同步运行模式）。  
  
 关闭事务安全可将会话切换到异步运行模式，该模式可使性能达到最佳。 主体不可用时镜像将停止，但它可以作为备用使用（故障转移需要使用可能会丢失数据的强制服务）。  
  
### <a name="to-turn-on-transaction-safety"></a>打开事务安全  
  
1.  连接到主体服务器。  
  
2.  发出以下 Transact-SQL 语句：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     其中，\<database> 为镜像数据库的名称。  
  
### <a name="to-turn-off-transaction-safety"></a>关闭事务安全  
  
1.  连接到主体服务器。  
  
2.  发出以下语句：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     其中，\<database> 为镜像数据库。  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [数据库镜像运行模式](database-mirroring-operating-modes.md)  
  
  
