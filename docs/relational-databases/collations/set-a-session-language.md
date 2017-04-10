---
title: "设置会话语言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "错误 [SQL Server], 国际注意事项"
  - "全球化 [SQL Server], 会话"
  - "时间 [SQL Server]"
  - "会话 [SQL Server], 语言"
  - "国际注意事项 [SQL Server], 会话"
  - "日期 [SQL Server], 会话语言"
  - "全球注意事项 [SQL Server], 会话"
  - "客户端会话语言"
  - "时间 [SQL Server], 会话语言"
  - "消息 [SQL Server], 国际注意事项"
  - "服务器端会话语言"
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 设置会话语言
  根据语言和区域性首选项，可用会话语言设置下列元素在服务器上显示的方式：  
  
-   用于显示错误和其他系统消息的语言。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用的所有语言中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持所有系统错误字符串和系统错误消息拥有多个副本。 可以在 [sys.messages](../Topic/sys.messages%20\(Transact-SQL\).md) 目录视图中查看这些消息。 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本时，这些系统消息被翻译成所安装的语言版本。 默认情况下，也可以获得这些消息的美国英语集。 此外，可以使用 [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md) 添加特定语言的用户定义消息。  
  
-   日期和时间数据的格式。  
  
-   日和月的名称，包括缩写。  
  
-   周的第一天。  
  
-   货币数据。  
  
 有 33 种语言可用于会话设置。 有关语言列表，请参阅 [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。  
  
## 从服务器设置会话语言  
 若要从服务器设置会话语言，请使用 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)。  
  
## 从客户端设置会话语言  
 可以用 OLE DB、ODBC 或 ADO.NET 在客户端设置会话语言。 对于 OLE DB，请使用 SSPROP_INIT_CURRENTLANGUAGE 属性。 有关详细信息，请参阅[初始化和授权属性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
 对于 ODBC，请使用语言关键字。 有关详细信息，请参阅 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)。  
  
 对于 ADO.NET，请使用 **ConnectionString** 对象的 **Current Language** 参数。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC) 软件开发包 (SDK) 文档。  
  
  