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
manager: craigg
ms.openlocfilehash: dddd5da66f09226579a6366baa1a16a6ab00d6bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094185"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>无效的命名管道名称会妨碍升级
  如果 named pipes 协议配置得不正确，则升级将失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 在升级过程中，安装程序将[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]启动具有 shared memory 支持的实例，该实例只接受本地连接。 如果在服务器上指定的管道名称不为空，则它必须以字符串 "\\\\.\pipe\\" 开头才能有效。 如果管道名称无效，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将不启动，并且安装将失败。  
  
## <a name="corrective-action"></a>纠正措施  
 使用** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]网络实用工具**来提供有效的管道名称，然后运行安装程序。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
