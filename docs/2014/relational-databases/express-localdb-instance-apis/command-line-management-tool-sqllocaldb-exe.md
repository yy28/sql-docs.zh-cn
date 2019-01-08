---
title: 命令行管理工具：SqlLocalDB.exe |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ea983555fdcb4bb177813db88d40f4bcc59c0e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765469"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>命令行管理工具：SqlLocalDB.exe
  SqlLocalDB.exe 是一个简单的工具，它使用户能够从命令行轻松管理 LocalDB 实例。 它作为 LocalDB 实例 API 的简单包装实现。 与在很多类似的 SQL Server 工具（例如 SQLCMD）中一样，参数作为命令行参数传递给 SqlLocalDB，并且将输出发送到控制台。  
  
 借助于 SqlLocalDB，开发人员不必编写代码或依赖于其他工具来调用 API，即可使用 LocalDB。  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB 选项  
 SqlLocalDB 支持以下选项。  
  
|选项|作用|  
|------------|------------------|  
|`-?`|打印帮助文本。|  
|`create&#124;c "instance name" [version-number] [-s]`|创建具有指定名称和版本的新 LocalDB 实例。<br /><br /> 如果省略 [version-number] 参数，则它默认为 SqlLocalDB 内部版本。<br /><br /> -s 在创建新的 LocalDB 实例后启动它。|  
|`delete&#124;d "instance name"`|删除具有指定名称的 LocalDB 实例。|  
|`start&#124;s "instance name"`|启动具有指定名称的 LocalDB 实例。|  
|`stop&#124;p "instance name" [-i&#124;-k]`|当前查询完成运行后，停止具有指定名称的 LocalDB 实例。<br /><br /> -i 请求使用 NOWAIT 选项关闭 LocalDB 实例。<br /><br /> -k 终止 LocalDB 实例进程而不联系它。|  
|`share&#124;h ["owner SID or account"] "private name" "shared name"`|使用指定的共享名称共享指定的私有实例。 如果省略该用户 SID 或帐户名称，则默认为当前用户。|  
|`unshare&#124;u "shared name"`|不共享指定的共享 LocalDB 实例。|  
|`info&#124;i`|列出当前用户拥有的所有现有 LocalDB 实例和所有共享的 LocalDB 实例。|  
|`info&#124;i "instance name"`|打印有关指定的 LocalDB 实例的信息。|  
|`versions&#124;v`|列出计算机上安装的所有 LocalDB 版本。|  
|||  
|`trace&#124;t on&#124;off`|打开和关闭跟踪。|  
  
 SqlLocalDB 将空格作为分隔符；必须将包含空格和特殊字符的实例名称用引号引起来。 例如：  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
