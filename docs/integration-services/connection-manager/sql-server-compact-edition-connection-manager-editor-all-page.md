---
title: "SQL Server Compact Edition 连接管理器编辑器（“全部”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sqlmobileconnection.all.f1"
helpviewer_keywords: 
  - "SQL Server Compact 连接管理器编辑器"
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# SQL Server Compact Edition 连接管理器编辑器（“全部”页）
  可以使用 **“SQL Server Compact Edition 连接管理器”** 对话框，指定连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库时使用的属性。  
  
 若要了解有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 连接管理器的详细信息，请参阅 [SQL Server Compact Edition 连接管理器](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)。  
  
## 选项  
 **自动收缩阈值**  
 指定运行自动收缩进程前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库中允许使用的可用空间大小（以百分比表示）。  
  
 **默认锁升级**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库在尝试升级锁之前获取的数据库锁的数量。  
  
 **默认锁超时值**  
 指定事务等待锁的默认时间间隔（毫秒）。  
  
 **刷新间隔**  
 指定提交的事务将数据刷新到磁盘的时间间隔（秒）。  
  
 **区域设置标识符**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库的区域设置 ID (LCID)。  
  
 **最大缓冲区大小**  
 指定在将数据刷新到磁盘之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 使用的最大内存量 (KB)。  
  
 **最大数据库大小**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库的最大大小 (MB)。  
  
 **模式**  
 指定打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库的文件模式。 此属性的默认值为 **“读写”**。  
  
 “模式”选项包含四个值，如下表所述：  
  
|“值”|Description|  
|-----------|-----------------|  
|**只读**|指定对数据库的只读访问。|  
|**“读写”**|指定对数据库的读/写权限。|  
|**排他**|指定对数据库的排他访问。|  
|**共享读取**|指定其他用户可以同时读取该数据库。|  
  
 **持久性安全信息**  
 指定安全信息是否作为连接字符串的一部分返回。 此选项的默认值为 **False**。  
  
 **临时文件目录**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 临时数据库文件的位置。  
  
 **数据源**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库的名称。  
  
 **密码**  
 输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库的密码。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [SQL Server Compact Edition 连接管理器编辑器（“连接”页）](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  