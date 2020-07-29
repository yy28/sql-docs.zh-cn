---
title: 验证所有订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 27b324de43f1aa9bc330057ca9159ccf78d0ce1b
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "87107452"
---
# <a name="validate-all-subscriptions"></a>验证所有订阅
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  可以使用 **“验证所有订阅”** 对话框，指定下次运行各个订阅的合并代理时应验证对合并发布的所有订阅。 验证的结果显示在复制监视器中。 有关详细信息，请参阅 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
 右键单击 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅，再单击 **“验证单个订阅”** ，也可以验证单个订阅。  
  
## <a name="options"></a>选项  
 **仅验证行计数**  
 选择此选项可以验证订阅服务器上的表是否与发布服务器上的表具有相同的行数。 此方法不会验证行的内容是否匹配。 行计数验证是一种简易验证方法，可帮助您了解数据是否存在问题。  
  
 **验证行计数并比较校验和以验证行数据**  
 除了可在发布服务器和订阅服务器上对行进行计数之外，还可使用二进制校验和算法来计算所有数据的校验和。 如果行计数失败，则不计算校验和。 此选项对 [!INCLUDE[ssEW](../../includes/ssew-md.md)]无效。  
  
## <a name="see-also"></a>另请参阅  
 [验证已复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
