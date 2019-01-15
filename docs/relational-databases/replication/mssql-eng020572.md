---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1a4b85368a0aa83909c0d05830c64631efe9027
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134187"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20572|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|在验证失败之后，订阅服务器“%s”对发布“%s”中项目“%s”的订阅已被重新初始化。|  
  
## <a name="explanation"></a>解释  
 根据发布服务器上的数据对订阅服务器上的数据进行验证，数据不匹配；因此验证失败。 在指定应该执行的验证时，选择了如果验证失败则应重新初始化订阅的选项。 重新初始化订阅包括在订阅服务器上应用新的快照。 有关验证的详细信息，请参阅 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
## <a name="user-action"></a>用户操作  
 在订阅服务器上应用了新的快照后，发布服务器和订阅服务器上的数据将会匹配。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
