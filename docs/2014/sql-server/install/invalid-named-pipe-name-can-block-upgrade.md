---
title: 无效的命名的管道名称可能会妨碍升级 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c94c1eeff18bff698e2a6353e29b72dd33278d03
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024262"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>无效的命名管道名称会妨碍升级
  如果 named pipes 协议配置得不正确，则升级将失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 在升级期间，安装程序将启动[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]共享的内存支持的实例，只接受本地连接的命名的管道。 如果服务器上指定的管道名称不为空，它必须以字符串开头"\\\\。 \pipe\\"才能有效。 如果管道名称无效，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将不启动，并且安装将失败。  
  
## <a name="corrective-action"></a>纠正措施  
 使用**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]网络实用工具**要提供一个有效的管道名称，然后运行安装程序。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
