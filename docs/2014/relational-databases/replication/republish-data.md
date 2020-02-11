---
title: 重新发布数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- republishing data
- publishing [SQL Server replication], Subscribers
- Subscribers [SQL Server replication], republishing data
ms.assetid: a1485cf4-b1c4-49e9-ab06-8ccfaad998f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 976520f5000d3a0f96ee3bdea25bcc9802939d36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250416"
---
# <a name="republish-data"></a>重新发布数据
  在重新发布模式中，发布服务器将数据发送到订阅服务器，后者将数据重新发布到任意数目的其他订阅服务器。 当发布服务器必须通过低速或昂贵的通信链接向订阅服务器发送数据时，这很有用。 如果在链接的远端有许多订阅服务器，那么使用重新发布服务器可将大量分发负荷转移到链接的远端。  
  
 重新发布数据分为下列几个步骤：  
  
1.  在发布服务器上创建发布。  
  
2.  为重新发布的订阅服务器创建对发布的订阅。  
  
3.  初始化订阅。 必须先初始化订阅，才可在重新发布的订阅服务器上创建发布，否则复制将失败。  
  
4.  在重新发布的订阅服务器上的订阅数据库中创建发布。  
  
5.  在重新发布的订阅服务器上为其他订阅服务器创建对发布的订阅。  
  
6.  初始化订阅。  
  
> [!NOTE]  
>  如果在重新发布拓扑中使用合并复制，则所有重新发布的订阅服务器都必须使用服务器订阅。 有关订阅类型的详细信息，请参阅[订阅发布](subscribe-to-publications.md)。  
  
 在下图中，发布服务器和重新发布服务器都作为其自身的本地分发服务器。 如果将它们都设置为使用远程分发服务器，则各分发服务器需要与其发布服务器位于低速或昂贵的通信链接的同一端。 发布服务器必须通过可靠、高速的通信链接连接到远程分发服务器。  
  
 ![重新发布数据](media/repl-06a.gif "重新发布数据")  
  
 任何服务器都既可用作发布服务器又可用作订阅服务器。 例如，考虑一下下面这个关系图：表的发布位于伦敦，且必须分发到美国四个不同的城市，即芝加哥、纽约、圣地亚哥和西雅图。 之所以选择位于纽约的服务器来订阅源于伦敦的已发布表，是因为纽约的站点满足下列条件：  
  
-   返回伦敦的网络链接相对可靠。  
  
-   伦敦到纽约的通信成本可以接受。  
  
-   从纽约到美国所有其他订阅服务器站点都有很好的网络通信线路。  
  
     ![将数据重新发布到分散位置](media/repl-06.gif "将数据重新发布到分散位置")  
  
 复制支持下表中显示的重新发布方案。  
  
|发布者|发布订阅服务器|订阅者|  
|---------------|---------------------------|----------------|  
|事务发布|事务订阅/事务发布|事务订阅|  
|事务发布|事务订阅/合并发布<sup>1</sup>|合并订阅|  
|合并发布|合并订阅/合并发布|合并订阅|  
|合并发布|合并订阅/事务发布|事务订阅|  
  
 <sup>1</sup>应在合并发布`@published_in_tran_pub`上设置属性。 默认情况下，事务复制将订阅服务器上的表视为只读。 如果合并复制对事务订阅中的表进行了数据更改，则可能发生数据无法收敛的情况。 为避免这种风险，建议您在合并发布中将所有此类表都指定为仅供下载。 这样可以防止合并订阅服务器向表中上载数据更改。 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
## <a name="see-also"></a>另请参阅  
 [“配置分发”](configure-distribution.md)   
 [发布数据和数据库对象](publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [初始化订阅](initialize-a-subscription.md)   
 [同步数据](synchronize-data.md)  
  
  
