---
title: "FileTable 架构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FileTable [SQL Server], 表架构"
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
caps.latest.revision: 7
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# FileTable 架构
  说明 FileTable 的预定义固定架构。  
  
|文件属性名称|type|Size|默认|说明|文件系统可访问性|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|变量|一个标识此项的位置的 **hierarchyid** 。|此节点在分层 FileNamespace 中的位置。<br /><br /> 表的主键。|可通过设置 Windows 路径值来创建和修改。|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||由 **NEWID()** 函数返回的值。|FILESTREAM 数据的唯一 ID。|不适用。|  
|**file_stream**|**varbinary(max)**<br /><br /> **文件流 (filestream)**|变量|NULL|包含 FILESTREAM 数据。|不适用。|  
|**file_type**|**nvarchar(255)**|变量|NULL。<br /><br /> 文件系统中的创建或重命名操作将从名称填充文件扩展名值。|表示文件的类型。<br /><br /> 在你创建全文索引时，可将此列用作 **TYPE COLUMN**。<br /><br /> **file_type** 是持久化计算列。|自动计算。 无法设置。|  
|**名称**|**nvarchar(255)**|变量|GUID 值。|文件或目录的名称。|可使用 Windows API 创建或修改。|  
|**parent_path_locator**|**hierarchyid**|变量|一个标识包含此项的目录的 **hierarchyid** 。|包含目录的 **hierarchyid** 。<br /><br /> **parent_path_locator** 是持久化计算列。|自动计算。 无法设置。|  
|**cached_file_size**|**bigint**|||FILESTREAM 数据的大小（以字节为单位）。<br /><br /> **cached_file_size** 是持久化计算列。|虽然缓存文件的大小会自动保持更新，但在特殊情况下也可能会出现不同步的问题。 若要计算确切的大小，请使用 **DATALENGTH()** 函数。|  
|**creation_time**|**datetime2(4)**<br /><br /> **非空**|8 字节|当前时间。|文件的创建日期和时间。|自动计算。 也可以通过使用 Windows API 设置。|  
|**last_write_time**|**datetime2(4)**<br /><br /> **非空**|8 字节|当前时间。|上次更新文件的日期和时间。|自动计算。 也可以通过使用 Windows API 设置。|  
|**last_access_time**|**datetime2(4)**<br /><br /> **非空**|8 字节|当前时间。|上次访问文件的日期和时间。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_directory**|**bit**<br /><br /> **非空**|1 字节|FALSE|指示行是否表示目录。 此值由系统自动计算，无法设置。|自动计算。 无法设置。|  
|**is_offline**|**bit**<br /><br /> **非空**|1 字节|FALSE|脱机文件属性。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_hidden**|**bit**<br /><br /> **非空**|1 字节|FALSE|隐藏文件属性。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_readonly**|**bit**<br /><br /> **非空**|1 字节|FALSE|只读文件属性。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_archive**|**bit**<br /><br /> **非空**|1 字节|FALSE|存档属性。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_system**|**bit**<br /><br /> **非空**|1 字节|FALSE|系统文件属性。|自动计算。 也可以通过使用 Windows API 设置。|  
|**is_temporary**|**bit**<br /><br /> **非空**|1 字节|FALSE|临时文件属性。|自动计算。 也可以通过使用 Windows API 设置。|  
  
## 另请参阅  
 [创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  