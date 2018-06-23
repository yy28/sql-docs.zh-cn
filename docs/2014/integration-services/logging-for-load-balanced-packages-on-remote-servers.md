---
title: 日志记录的负载平衡远程服务器上的包 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 85f423c0d8b194a73042e808326d3ce28ef1de0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027024"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>远程服务器上的负载平衡包的日志记录
  如果所有子包都使用相同的日志提供程序并且它们全部写入相同的目标，则管理员更容易管理在各个服务器上运行的所有子包的日志。 创建所有子包公用日志文件的一种方式是：将子包配置为“将子包事件记录到 SQL Server 日志提供程序”。 可以将所有包配置为使用相同的数据库、相同的服务器和相同的服务器实例。  
  
 若要查看日志文件，管理员只须登录到单个服务器上，即可查看所有子包的日志文件。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在包中启用日志记录的信息，请参阅 [在 SQL Server Data Tools 中启用包日志记录](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 日志记录](performance/integration-services-ssis-logging.md)  
  
  