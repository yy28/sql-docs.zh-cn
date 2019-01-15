---
title: 订阅验证选项（事务订阅）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10d1920a4205bb1ec258c0b81303b2b61a50cb1f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123627"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>订阅验证选项（事务订阅）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 **“订阅验证选项”** 对话框可以指定是仅使用行计数进行验证，还是使用行计数和二进制校验和进行验证。  
  
## <a name="options"></a>选项  
 **验证订阅服务器与发布服务器具有相同的复制数据行数**  
 选择要执行的行计数验证的类型。 对于 Oracle 发布， **“通过直接查询表计算实际的行计数”** 是唯一可用的选项。  
  
 **比较校验和以验证行数据**  
 除了可在发布服务器和订阅服务器上对行进行计数之外，还可使用二进制校验和算法来计算所有数据的校验和。 如果行计数失败，则不计算校验和。  
  
 **完成验证后停止运行分发代理**  
 默认情况下，分发代理会连续运行。 选择此选项可以在执行验证之后停止运行代理。 这样，就可以在继续将数据复制到订阅服务器之前检查验证是否成功。  
  
## <a name="see-also"></a>另请参阅  
 [验证订阅服务器上的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
