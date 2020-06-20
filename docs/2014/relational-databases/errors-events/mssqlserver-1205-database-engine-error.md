---
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4df3e6edc789dfc95e41cec0b516fb335aa9a823
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968009"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1205|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LK_VICTIM|  
|消息正文|事务(进程 ID %d)与另一个进程被死锁在 %.*ls 资源上，并且已被选作死锁牺牲品。 重新运行该事务。|  
  
## <a name="explanation"></a>说明  
 在单独的事务上以相互冲突的顺序访问资源，从而导致死锁。 例如：  
  
-   Transaction1 更新 **Table1.Row1**，而 Transaction2 更新 **Table2.Row2**。  
  
-   Transaction1 尝试更新 **Table2.Row2**，但因 Transaction2 尚未提交而被阻止。  
  
-   Transaction2 现在尝试更新 **Table1.Row1**，但因 Transaction1 尚未提交而被阻止。  
  
-   之所以出现死锁，是因为 Transaction1 在等待 Transaction2 完成，但 Transaction2 在等待 Transaction1 完成。  
  
 系统将检测到此死锁并将选择其中一个作为“受害者”的事务，并将发出此消息，回滚受害者的事务。  
  
## <a name="user-action"></a>用户操作  
 重新执行事务。 您还可以修订应用程序以避免死锁。 可以重试被选作牺牲品的事务，而且很可能成功，具体取决于同时执行的操作。  
  
 为防止或避免出现死锁，请考虑让所有的事务按相同顺序（先访问 **Table1**，然后访问 **Table2**）访问行；这样，虽然可能会出现阻止，但不会出现死锁。  
  
  
