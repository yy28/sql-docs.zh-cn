---
title: 设置排队更新冲突解决选项 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 32
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d4b372dc750822d965474d93d40ff7911cf0cf7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026311"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>设置排队更新冲突解决选项 (SQL Server Management Studio)
  在“发布属性 - \<发布>”对话框的“订阅选项”页上，为支持排队更新订阅的发布设置冲突解决选项。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>设置排队更新冲突解决选项  
  
1.  在“发布属性 - \<发布>”对话框的“订阅选项”页上，为“冲突解决策略”选项选择以下值之一：  
  
    -   **保留发布服务器更改**  
  
    -   **保留订阅服务器更改**  
  
    -   **重新初始化订阅**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [允许更新事务发布的订阅](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  