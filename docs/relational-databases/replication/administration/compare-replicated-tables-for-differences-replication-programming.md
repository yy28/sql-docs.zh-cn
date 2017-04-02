---
title: "比较所复制表的差异（复制编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "tablediff 实用工具"
  - "比较复制的表"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 比较所复制表的差异（复制编程）
  项目验证用于确定发布服务器和订阅服务器上的表项目的已发布数据是否不同，这可能表明无法收敛。 有关详细信息，请参阅 [验证已复制数据](../../../relational-databases/replication/validate-replicated-data.md)。 但是，验证仅返回通过或失败信息，而不会提供任何有关源表和目标表之间存在哪些差异的信息。 **tablediff** 命令提示实用工具返回两个表之间存在的详细差异信息，甚至可生成 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本，以使订阅与发布服务器上的数据实现收敛。  
  
> [!NOTE]  
>   **Tablediff** 实用程序仅支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务器。  
  
### 使用 tablediff 比较复制的表之间的不同  
  
1.  从复制拓扑中任何服务器的命令提示符处，运行 [tablediff Utility](../../../tools/tablediff-utility.md)。 指定下列参数：  
  
    -   **-sourceserver** -服务器在其数据已知正确无误，通常为发布服务器的名称。  
  
    -   **-sourcedatabase** -包含正确的数据的数据库的名称。  
  
    -   **-sourcetable** -要比较的项目的源表的名称。  
  
    -   （可选） **-sourceschema** -源表的表，如果不是默认架构的架构所有者。  
  
    -   （可选） **-sourceuser** 和 **-sourcepassword** 在使用 SQL Server 身份验证连接到发布服务器。  
  
        > [!IMPORTANT]  
        >  请尽可能使用 Windows 身份验证。 如果必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，则在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
    -   **-destinationserver** -服务器在其要在比较数据时，通常订阅服务器的名称。  
  
    -   **-destinationdatabase** -名称的要比较的数据库。  
  
    -   **-destinationtable** -要比较的表的名称。  
  
    -   （可选） **-destinationschema** -目标表中，如果不是默认架构的架构所有者。  
  
    -   （可选） **-destinationuser** 和 **-destinationpassword** 时使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到订阅服务器上。  
  
        > [!IMPORTANT]  
        >  请尽可能使用 Windows 身份验证。 如果必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，则在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
    -   （可选）使用 **-c** 来执行列级比较。  
  
    -   （可选）使用 **-q** 来执行快速，行计数的和仅限架构的比较。  
  
    -   （可选）指定的文件名和路径 **-o** 若要将结果输出到一个文件。  
  
    -   （可选）要插入的结果到其中的订阅数据库中指定的表 **-et**。 如果该表已经存在，请指定 **-dt** 以首先删除表。  
  
    -   （可选）使用 **-f** 生成 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 文件以修复在订阅服务器上的数据，以使其与发布服务器上的数据匹配。 使用 **-df** 以指定的数 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 每个文件中的语句。  
  
    -   （可选）使用 **-rc** 和 **-ri** 若要指定某一操作和重试时间间隔重试的次数。  
  
    -   （可选）使用 **-严格** 以强制实施严格的架构源和目标表之间的比较。  
  
## 另请参阅  
 [在订阅服务器上验证数据](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  