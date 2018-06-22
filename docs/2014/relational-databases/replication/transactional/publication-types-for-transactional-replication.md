---
title: 事务复制的发布类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 11e9e6ffafe62c66684470b4b04e2e0b67cc868b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016327"
---
# <a name="publication-types-for-transactional-replication"></a>事务复制的发布类型
  事务复制提供了三种发布类型：  
  
|发布类型|Description|  
|----------------------|-----------------|  
|标准事务发布|适合于订阅服务器上的所有数据均为只读的拓扑（事务复制在订阅服务器上并不强制如此）。<br /><br /> 默认情况下，在使用 Transact-SQL 或复制管理对象 (RMO) 时创建标准事务发布。 使用新建发布向导时，将通过选择 **“发布类型”** 页上的 **“事务发布”** 来创建标准事务发布。<br /><br /> 有关创建发布的详细信息，请参阅 [发布数据和数据库对象](../publish/publish-data-and-database-objects.md)。|  
|对等拓扑中的事务发布|此发布类型的特征如下：<br /><br /> 每个位置都具有相同的数据，兼作发布服务器和订阅服务器。<br /><br /> 同一行每次只能在一个位置进行更改。<br /><br /> 此拓扑最适合需要高可用性和读取可伸缩性的服务器环境。<br /><br /> <br /><br /> 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)。|  
  
## <a name="see-also"></a>请参阅  
 [事务复制](transactional-replication.md)  
  
  