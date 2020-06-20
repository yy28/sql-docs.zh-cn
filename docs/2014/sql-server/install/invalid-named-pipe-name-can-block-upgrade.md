---
title: 无效的命名管道名称可以阻止升级 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: bacfd3d097d7cccb0a5780328c4db95dc5afc733
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059253"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>无效的命名管道名称会妨碍升级
  如果 named pipes 协议配置得不正确，则升级将失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 在升级过程中，安装程序将启动 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 具有 shared memory 支持的实例，该实例只接受本地连接。 如果在服务器上指定的管道名称不为空，则它必须以字符串 " \\ \\ .\pipe \\ " 开头才能有效。 如果管道名称无效，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将不启动，并且安装将失败。  
  
## <a name="corrective-action"></a>纠正措施  
 使用** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 网络实用工具**来提供有效的管道名称，然后运行安装程序。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
