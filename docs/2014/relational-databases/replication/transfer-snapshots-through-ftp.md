---
title: 通过 FTP 传输快照 | Microsoft Docs
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
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 39
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a634b0cf961d922ea3169f5c44aa7c87f3ec42fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137951"
---
# <a name="transfer-snapshots-through-ftp"></a>通过 FTP 传输快照
  默认情况下，快照存储在定义为通用命名约定 (UNC) 共享的文件夹中。 复制还允许指定用文件传输协议 (FTP) 共享取代 UNC 共享。 若要使用 FTP，必须先配置 FTP 服务器，然后配置要使用 FTP 的发布和一个或多个订阅。 有关如何配置 FTP 服务器的详细信息，请参阅 Internet 信息服务 (IIS) 文档。 如果为发布指定了 FTP 信息，则对此发布的订阅将默认使用 FTP。 仅当运行 IIS 的计算机通过防火墙与分发服务器相隔离时，才会使用 FTP 进行 Web 同步。 在这种情况下，FTP 可用于传输来自分发服务器和运行 IIS 的计算机的快照。 （快照始终使用 HTTPS 传输到订阅服务器。）  
  
> [!IMPORTANT]  
>  我们建议您使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证和 UNC 共享而不要使用 FTP 共享，因为 FTP 密码必须存储，并且密码以纯文本格式从订阅服务器或运行 IIS 的计算机（当它使用 Web 同步时）发送到 FTP 服务器。 此外，因为是由单一帐户控制对快照共享的访问，所以不可能确保筛选的合并发布的订阅服务器仅可以从其数据分区访问快照文件。  
  
 若要通过 FTP 传递快照，请参阅 [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md)。  
  
## <a name="see-also"></a>请参阅  
 [合并复制的 Web 同步](web-synchronization-for-merge-replication.md)   
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)   
 [快照选项](snapshot-options.md)  
  
  