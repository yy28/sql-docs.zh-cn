---
title: 取消选项（Distributed Replay 管理工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce29f56d7877712dd99553968b364b1c33471c2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177319"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>Cancel 选项（分布式重播管理工具）
  Distributed Replay 管理工具`DReplay.exe`是一个命令行工具，可用于与 Distributed Replay 控制器进行通信。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本主题介绍 **cancel** 命令行选项和相应的语法。

 **cancel** 选项取消控制器上运行的当前操作。

 ![主题链接图标](../../database-engine/media/topic-link.gif "“主题链接”图标") 有关与此管理工具语法结合使用的语法约定的详细信息，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。

## <a name="syntax"></a>语法

```

dreplay cancel [-mcontroller] [-q] 
```

#### <a name="parameters"></a>parameters
 **-m** *控制器*控制器的计算机名称。 可以用“`localhost`”或“`.`”指代本地计算机。

 如果未指定 **-m** 参数，则使用本地计算机。

 **-q**安静模式。 不提示进行确认。

 **-q** 参数是可选的。

## <a name="examples"></a>示例
 在下面的示例中，在静默模式下提交一个取消请求。 值 `localhost` 表示控制器服务与管理工具在同一计算机上运行。

```
dreplay cancel -m localhost -q
```

## <a name="permissions"></a>权限
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。

 有关详细信息，请参阅 [Distributed Replay Security](distributed-replay-security.md)。

## <a name="see-also"></a>另请参阅
 [SQL Server 分布式重播](sql-server-distributed-replay.md)


