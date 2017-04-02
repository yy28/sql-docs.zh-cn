---
title: "重新生成自定义事务过程以反映架构更改 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "自定义过程 [SQL Server 复制]"
  - "事务复制, 复制架构更改"
  - "架构 [SQL Server 复制], 复制更改"
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 重新生成自定义事务过程以反映架构更改
  默认情况下，事务复制通过发布中的每个表项目的内部过程生成的存储过程，在订阅服务器上进行所有数据更改。 三个过程（分别对应插入、更新和删除）将复制到订阅服务器并在插入、更新或删除复制到订阅服务器后执行。 对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布服务器上的表进行架构更改后，复制会通过调用同一组内部脚本过程自动重新生成这些过程，以便新过程与新架构相匹配（Oracle 发布服务器不支持复制架构更改）。  
  
 也可以指定自定义过程来替换一个或多个默认过程。 如果架构更改将影响过程，则应该更改自定义过程。 例如，如果一个过程引用了架构更改中删除的列，则对此列的引用应从过程中删除。 复制有两种方式将新的自定义过程传播到订阅服务器：  
  
-   第一种选择是使用自定义脚本过程替换复制使用的默认过程：  
  
    1.  在执行时 [sp_addarticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), ，确保 **@schema_option** 0x02 位设置为 **true**。  
  
    2.  执行 [sp_register_custom_scripting & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) 将值指定为 'insert'、 'update' 或 'delete' 的参数和 **@type** 和自定义的名称编写脚本的参数的过程 **@value**。  
  
     下次进行架构更改时，复制会调用此存储过程为新用户定义的自定义存储过程编写定义脚本，然后将此过程传播到每个订阅服务器。  
  
-   第二种选择是使用包含新自定义过程定义的脚本：  
  
    1.  在执行时 [sp_addarticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), ，请设置 **@schema_option** 0x02 位设置为 **false** 以便复制不会自动生成订阅服务器上的自定义过程。  
  
    2.  每个架构更改之前, 创建新的脚本文件，并通过执行与复制注册脚本 [sp_register_custom_scripting & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)。 将值指定为参数 'custom_script' **@type** 和参数的发布服务器上的脚本的路径 **@value**。  
  
     下次进行相关的架构更改时，此脚本会在每个订阅服务器上、在 DDL 命令所在的事务内执行。 更改架构后，此脚本将撤消注册。 在后续架构更改后必须重新注册此脚本，使其执行。  
  
## 另请参阅  
 [指定如何传播事务项目的更改](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [对发布数据库进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  