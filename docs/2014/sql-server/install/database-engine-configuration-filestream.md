---
title: 数据库引擎配置-Filestream |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], about FILESTREAM
ms.assetid: 641a10a1-ae52-4d26-8f1c-a032a4aeff02
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 99fb929a9a3fdbdb643edeaf041d4cd74d64c75c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015388"
---
# <a name="database-engine-configuration---filestream"></a>数据库引擎配置 - 文件流
  使用此页可针对此 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装启用 FILESTREAM。 FILESTREAM 集成[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]使用 NTFS 文件系统通过将存储`varbinary(max)`二进制大型对象 (BLOB) 数据作为文件系统上的文件。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可插入、更新、查询、搜索和备份 FILESTREAM 数据。 通过 Win32 文件系统接口可以流式方式访问数据。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **针对 Transact-SQL 访问启用 FILESTREAM**  
 选中此项可针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。 必须选中此控制选项，才能使用其他控制选项。  
  
 **针对文件 I/O 流访问启用 FILESTREAM**  
 选中此项可针对 FILESTREAM 启用 Win32 流访问。  
  
 **Windows 共享名**  
 使用此控制选项可输入将用来存储 FILESTREAM 数据的 Windows 共享的名称。  
  
 **允许远程客户端针对 FILESTREAM 数据启用流访问**  
 选中此控制选项可允许远程客户端访问此服务器上的此 FILESTREAM 数据。  
  
## <a name="see-also"></a>请参阅  
 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
