---
title: 指定合并订阅类型和冲突解决优先级（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a19ae6246fe59308283fbaf2f35e2c49f96b140c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055560"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)
  可以在新建订阅向导的 **“订阅类型”** 页上指定合并订阅类型和冲突解决优先级。 有关使用此向导的详细信息，请参阅 [Create a Pull Subscription](create-a-pull-subscription.md) 和 [Create a Push Subscription](create-a-push-subscription.md)。  
  
 订阅类型在创建订阅后无法修改，但可以在 "**订阅属性- \<Publisher> ： \<PublicationDatabase> ** " 对话框中修改 "服务器" 订阅类型的优先级。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)。  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>指定合并订阅类型和冲突解决优先级  
  
1.  在新建订阅向导的 **“订阅类型”** 页上，为 **“订阅类型”** 选项选择 **“客户端”** 或 **“服务器”** 。  
  
2.  如果选择 **“服务器”** 订阅类型，还要输入 **“冲突解决的优先级”** 选项的值（0.00 到 99.99）。  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>修改冲突解决优先级  
  
1.  在**订阅属性- \<Publisher> ： \<PublicationDatabase> **在发布服务器上，为**Priority**选项输入值（0.00 到99.99）。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [高级合并复制冲突的检测和解决](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
