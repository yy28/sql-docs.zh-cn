---
title: "SQL Server Express LocalDB 实例 API 参考 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d01b87a26674a213c1c0ed0f14a6ff867222fc4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-express-localdb-reference---instance-apis"></a>SQL Server Express LocalDB 参考-实例 Api
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在传统的、 基于服务的 SQL Server 世界中，一台计算机上安装的单个 SQL Server 实例以物理方式分隔;即，每个实例必须安装和删除单独、 具有一组单独的二进制文件，并在单独的服务进程下运行。 SQL Server 实例名称用于指定用户要连接的 SQL Server 实例。  
  
 SQL Server Express LocalDB 实例 API 使用简化的“轻型”实例模型。 尽管各个 LocalDB 实例在磁盘和注册表中是单独分开的，但它们使用同一组共享 LocalDB 二进制代码。 此外，LocalDB 不使用服务；LocalDB 实例是通过 LocalDB 实例 API 调用按需启动的。 在 LocalDB 中，实例名称用于指定用户要使用的 LocalDB 实例。  
  
 LocalDB 实例始终由单个用户拥有，并且仅可从该用户的上下文中看到和访问，除非启用实例共享。  
  
 尽管从技术上说 LocalDB 实例与传统 SQL Server 实例不同，但它们的目标用途是类似的。 它们分别名*实例*来强调此相似性，并以使它们更直观到 SQL Server 用户。  
  
 LocalDB 支持两种类型的实例：自动实例 (AI) 和命名实例 (NI)。 LocalDB 实例的标识符为实例名称。  
  
## <a name="automatic-localdb-instances"></a>自动 LocalDB 实例  
 自动 LocalDB 实例是“公共的”；系统自动为用户创建和管理此类实例，并可由任何应用程序使用。 安装在用户计算机上的每个 LocalDB 版本都存在一个自动 LocalDB 实例。  
  
 自动 LocalDB 实例提供无缝的实例管理。 用户不需要创建该实例。 这使用户能够轻松地安装应用程序，并迁移到不同的计算机。 如果目标计算机已安装指定版本的 LocalDB，则该计算机也提供此版本的自动 LocalDB 实例。  
  
### <a name="automatic-instance-management"></a>自动实例管理  
 用户无需创建自动 LocalDB 实例。 在第一次使用此实例时将以惰性方式创建此实例，前提是用户计算机上提供了指定版本的 LocalDB。 从用户的角度来说，只要 LocalDB 存在，则自动实例始终存在。  
  
 其他实例管理操作（如删除、共享和取消共享）也适应于自动实例。 尤其是，删除自动实例可以高效地重置实例，这样，在下一个启动操作时将重新创建此实例。 如果系统数据库已损坏，则可能需要删除自动实例。  
  
### <a name="automatic-instance-naming-rules"></a>自动实例命名规则  
 自动 LocalDB 实例具有属于保留命名空间的特殊实例名称模式。 这对于防止名称与命名 LocalDB 实例发生冲突至关重要。  
  
 自动实例名称是以单个“v”字符为前缀的 LocalDB 基准版本号。 这看起来就是“v”加上两个数字且在两个数字之间有一个句点；例如，v11.0 或 V12.00。  
  
 非法自动实例名称的示例如下：  
  
-   11.0（开头缺少“v”字符）  
  
-   v11（缺少句点和版本的第二个数字）  
  
-   v11. （缺少版本的第二个数字）  
  
-   v11.0.1.2（版本号超出两个部分）  
  
## <a name="named-localdb-instances"></a>命名的 LocalDB 实例  
 命名的 LocalDB 实例是“私有的”；实例由负责创建和管理该实例的单个应用程序所拥有。 命名的 LocalDB 实例提供隔离并改进性能。  
  
### <a name="named-instance-creation"></a>创建命名实例  
 用户必须通过 LocalDB 管理 API 显式创建命名实例，或通过托管应用程序的 app.config 文件隐式创建命名实例。 托管应用程序也可以使用 API。  
  
 每个命名实例都具有关联的 LocalDB 版本；也就是说，它指向指定的一组 LocalDB 二进制代码。 命名实例的版本是在实例创建过程中设置的。  
  
### <a name="named-instance-naming-rules"></a>命名实例命名规则  
 为 128 个字符的总共最多可以有 LocalDB 实例名称 (默认情况下，限制通过**sysname**数据类型)。 这与传统 SQL Server 实例名称相比有显著差异，后者限制为 16 个 ASCII 字符的 NetBIOS 名称。 存在此差异的原因是 LocalDB 将数据库视为文件，因此，这意味着基于文件的语义，这样，它对于用户是直观的，可以更自由地选择实例名称。  
  
 LocalDB 实例名称可包含在文件名组分内合法的任何 Unicode 字符。 文件名组件中的有非法字符通常包括下列字符： ASCII/Unicode 字符 1 到 31，以及引号 （"），小于 (\<)、 大于 (>)、 竖线 (|)、 退格符 (\b)、 制表符 (\t)、 冒号 （:）、 星号 （*）问号 （？）、 反斜杠 (\\)，并正斜杠 （/）。 请注意，允许使用 Null 字符 (\ 0)，因为它用于终止字符串；第一个 Null 字符之后的任何字符都将忽略。  
  
> [!NOTE]  
>  非法字符列表取决于操作系统，并且可能在将来的版本中更改。  
  
 实例名称中的前导和尾随空格都将被忽略，并将进行修整。  
  
 若要避免命名冲突，名为 LocalDB 实例不能将遵循命名模式自动实例的名称作为前面所述"自动实例命名规则。" 尝试创建具有此名称的有效地遵循以下命名模式： 自动实例的命名的实例创建一个默认实例。  
  
## <a name="sql-server-express-localdb-reference-topics"></a>SQL Server Express LocalDB 参考主题  
 [SQL Server Express LocalDB 标头信息和版本信息](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
 提供用于查找 LocalDB 实例 API 的头文件信息和注册表项。  
  
 [命令行管理工具：SqlLocalDB.exe](../../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
 介绍 SqlLocalDB.exe，这是一个从命令行管理 LocalDB 实例的工具。  
  
 [LocalDBCreateInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbcreateinstance-function.md)  
 描述创建新的 LocalDB 实例的函数。  
  
 [LocalDBDeleteInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbdeleteinstance-function.md)  
 描述删除 LocalDB 实例的函数。  
  
 [LocalDBFormatMessage 函数](../../relational-databases/express-localdb-instance-apis/localdbformatmessage-function.md)  
 描述返回 LocalDB 错误的本地化说明的函数。  
  
 [LocalDBGetInstanceInfo 函数](../../relational-databases/express-localdb-instance-apis/localdbgetinstanceinfo-function.md)  
 描述获取有关 LocalDB 实例的信息的函数，如该实例是否存在、版本信息、是否正在运行等。  
  
 [LocalDBGetInstances 函数](../../relational-databases/express-localdb-instance-apis/localdbgetinstances-function.md)  
 描述返回具有指定版本的所有 LocalDB 实例的函数。  
  
 [LocalDBGetVersionInfo 函数](../../relational-databases/express-localdb-instance-apis/localdbgetversioninfo-function.md)  
 描述返回指定的 LocalDB 版本的信息的函数。  
  
 [LocalDBGetVersions 函数](../../relational-databases/express-localdb-instance-apis/localdbgetversions-function.md)  
 描述返回计算机上可用的所有 LocalDB 版本的函数。  
  
 [LocalDBShareInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbshareinstance-function.md)  
 描述共享指定的 LocalDB 实例的函数。  
  
 [LocalDBStartInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbstartinstance-function.md)  
 描述启动指定的 LocalDB 实例的函数。  
  
 [LocalDBStartTracing 函数](../../relational-databases/express-localdb-instance-apis/localdbstarttracing-function.md)  
 描述为用户启用 API 跟踪的函数。  
  
 [LocalDBStopInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbstopinstance-function.md)  
 描述停止指定的 LocalDB 实例运行的函数。  
  
 [LocalDBStopTracing 函数](../../relational-databases/express-localdb-instance-apis/localdbstoptracing-function.md)  
 描述为用户禁用 API 跟踪的函数。  
  
 [LocalDBUnshareInstance 函数](../../relational-databases/express-localdb-instance-apis/localdbunshareinstance-function.md)  
 描述停止共享指定的 LocalDB 实例的函数。  
  
  
