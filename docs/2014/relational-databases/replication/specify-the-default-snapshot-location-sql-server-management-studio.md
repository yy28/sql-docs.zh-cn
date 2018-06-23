---
title: 指定默认快照位置 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a5ed18727ebc0cea2783f81d071758b9b71265c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014048"
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>指定默认快照位置 (SQL Server Management Studio)
  可以在配置分发向导的 **“快照文件夹”** 页上指定默认快照位置。 有关使用此向导的详细信息，请参阅[配置发布和分发](configure-publishing-and-distribution.md)。 如果在未配置为分发服务器的服务器上创建发布，请在新建发布向导的 **“快照文件夹”** 页上指定默认快照位置。 有关使用此向导的详细信息，请参阅[创建发布](publish/create-a-publication.md)。  
  
 在“分发服务器属性 - \<分发服务器>”对话框的“发布服务器”页上，修改默认快照位置。 有关详细信息，请参阅[查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)。 在“发布属性 - \<发布>”对话框中设置每个发布的快照文件夹。 有关详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
### <a name="to-modify-the-default-snapshot-location"></a>修改默认快照位置  
  
1.  在“分发服务器属性 - \<分发服务器>”对话框的“发布服务器”页上，单击要更改其默认快照位置的发布服务器的属性按钮 (**…**)。  
  
2.  在“分发服务器属性 - \<分发服务器>”对话框中，为“默认快照文件夹”属性输入一个值。  
  
    > [!NOTE]  
    >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](security/secure-the-snapshot-folder.md)。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [备用快照文件夹位置](alternate-snapshot-folder-locations.md)   
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)  
  
  