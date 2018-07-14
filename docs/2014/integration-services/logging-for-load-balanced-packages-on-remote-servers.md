---
title: 负载的日志记录上平衡包的远程服务器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
caps.latest.revision: 23
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4a8aae457611e43419c75a348541e7dbd1ca004
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264973"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>远程服务器上的负载平衡包的日志记录
  如果所有子包都使用相同的日志提供程序并且它们全部写入相同的目标，则管理员更容易管理在各个服务器上运行的所有子包的日志。 创建所有子包公用日志文件的一种方式是：将子包配置为“将子包事件记录到 SQL Server 日志提供程序”。 可以将所有包配置为使用相同的数据库、相同的服务器和相同的服务器实例。  
  
 若要查看日志文件，管理员只须登录到单个服务器上，即可查看所有子包的日志文件。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在包中启用日志记录的信息，请参阅 [在 SQL Server Data Tools 中启用包日志记录](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 日志记录](performance/integration-services-ssis-logging.md)  
  
  
