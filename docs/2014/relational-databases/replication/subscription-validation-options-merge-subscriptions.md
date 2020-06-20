---
title: 订阅验证选项（合并订阅）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 458da0387dbaa1b366348c374748c42946893feb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063747"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>订阅验证选项（合并订阅）
  可以使用 **“订阅验证选项”** 对话框指定是仅使用行计数进行验证，还是使用行计数和二进制校验和进行验证。  
  
## <a name="options"></a>选项  
 **仅验证行计数**  
 选择此选项可以验证订阅服务器上的表是否与发布服务器上的表具有相同的行数。 此方法不会验证行的内容是否匹配。 行计数验证是一种简易验证方法，可帮助您了解数据是否存在问题。  
  
 **验证行计数并比较校验和以验证行数据**  
 除了可在发布服务器和订阅服务器上对行进行计数之外，还可使用二进制校验和算法来计算所有数据的校验和。 如果行计数失败，则不计算校验和。 此选项对无效 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [验证订阅服务器上的数据](validate-data-at-the-subscriber.md)   
 [验证已复制的数据](validate-data-at-the-subscriber.md)  
  
  
