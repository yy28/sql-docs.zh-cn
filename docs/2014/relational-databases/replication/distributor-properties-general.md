---
title: 分发服务器属性，常规 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a92d36dab69d6602fa9397473ee77133affe80f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128041"
---
# <a name="distributor-properties-general"></a>分发服务器属性，常规
  使用 **“分发服务器属性”** 对话框的 **“常规”** 页，可以添加和删除分发数据库，以及设置分发数据库属性。  
  
 分发数据库用于存储所有类型复制的元数据和历史记录数据，并存储事务复制的事务。 在许多情况下，单个分发数据库就能够满足需要。 不过，如果多个发布服务器使用单个分发服务器，则应考虑为每个发布服务器都创建一个分发数据库。 这样可确保通过每个分发数据库的数据流是不同的。  
  
## <a name="options"></a>“常规”  
 **数据库**  
 **“数据库”** 属性网格显示了分发服务器上分发数据库的名称和保持期属性。 **“事务保持期”** 是指为事务复制存储事务的时间长度（事务保持期也称为分发保持期）。 **“历史记录保持期”** 是指为所有类型的复制存储历史记录元数据的时间长度。 有关分发保持期的详细信息，请参阅[订阅过期和停用](subscription-expiration-and-deactivation.md)。  
  
 单击 **“数据库”** 属性网格中的属性按钮 ( **...** ) 可启动 **“分发数据库属性”** 对话框。  
  
 **新建**  
 单击此项可创建一个新的分发数据库。  
  
 **删除**  
 选择 **“数据库”** 属性网格中的一个现有分发数据库，再单击 **“删除”** ，即可删除该数据库。 如果只有一个这样的分发数据库，则无法删除；每个分发服务器必须至少有一个分发数据库。 若要删除所有分发数据库，则必须在该计算机上禁用分发功能。 有关详细信息，请参阅[禁用发布和分发](disable-publishing-and-distribution.md)。  
  
 **默认配置文件**  
 单击此项可访问 **“代理配置文件”** 对话框中的复制代理配置文件。 有关配置文件的详细信息，请参阅 [Replication Agent Profiles](agents/replication-agent-profiles.md)。  
  
## <a name="see-also"></a>请参阅  
 [“配置分发”](configure-distribution.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)  
  
  