---
title: "命令行管理工具： SqlLocalDB.exe |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8f2bac1f105f5d299fa97d11fa579226026134aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>命令行管理工具：SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SqlLocalDB.exe 是一个简单工具，使用户能够轻松地从命令行管理 LocalDB 实例。 它作为 LocalDB 实例 API 的简单包装实现。 与在很多类似的 SQL Server 工具（例如 SQLCMD）中一样，参数作为命令行参数传递给 SqlLocalDB，并且将输出发送到控制台。  
  
 借助于 SqlLocalDB，开发人员不必编写代码或依赖于其他工具来调用 API，即可使用 LocalDB。  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB 选项  
 SqlLocalDB 支持以下选项。  
  
|选项|作用|  
|------------|------------------|  
|`-?`|打印帮助文本。|  
|create\|c"实例名称"[版本号] [-s]|创建具有指定名称和版本的新 LocalDB 实例。<br /><br /> 如果省略 [version-number] 参数，则它默认为 SqlLocalDB 内部版本。<br /><br /> -s 在创建新的 LocalDB 实例后启动它。|  
|delete\|"实例名称"d|删除具有指定名称的 LocalDB 实例。|  
|用户|"实例名称"s|启动具有指定名称的 LocalDB 实例。|  
|停止|p"实例名称"[-i\|-k]|当前查询完成运行后，停止具有指定名称的 LocalDB 实例。<br /><br /> -i 请求使用 NOWAIT 选项关闭 LocalDB 实例。<br /><br /> -k 终止 LocalDB 实例进程而不联系它。|  
|share\|h ["所有者 SID 或帐户"]"私有""共享的名称"|使用指定的共享名称共享指定的私有实例。 如果省略该用户 SID 或帐户名称，则默认为当前用户。|  
|unshare\|"共享的名称"u|不共享指定的共享 LocalDB 实例。|  
|info\|我|列出当前用户拥有的所有现有 LocalDB 实例和所有共享的 LocalDB 实例。|  
|info\|"实例名称"i|打印有关指定的 LocalDB 实例的信息。|  
|versions\|v|列出计算机上安装的所有 LocalDB 版本。|  
|||  
|trace\|t on\|关闭|打开和关闭跟踪。|  
  
 SqlLocalDB 将空格作为分隔符；必须将包含空格和特殊字符的实例名称用引号引起来。 例如：  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
