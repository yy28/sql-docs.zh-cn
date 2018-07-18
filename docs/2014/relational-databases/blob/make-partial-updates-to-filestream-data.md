---
title: 对 FILESTREAM 数据进行部分更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de844f92f9ae7a35327defd4abcff3da9821ba66
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209187"
---
# <a name="make-partial-updates-to-filestream-data"></a>对 FILESTREAM 数据进行部分更新
  应用程序使用 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 对 FILESTREAM BLOB 数据进行部分更新。 [DeviceIoControl](http://go.microsoft.com/fwlink/?LinkId=105527) 函数将此值和从 [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) 返回的句柄传递到 FILESTREAM 驱动程序。 然后，该驱动程序将当前的 FILESTREAM 数据从服务器端强制复制到该句柄所引用的文件。 如果应用程序在已写入句柄后发出 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 值，则保留最后一个写入操作，但之前对该句柄执行的写入操作将丢失。  
  
> [!NOTE]  
>  FILESTREAM 依赖于 [SMB 协议](http://go.microsoft.com/fwlink/?LinkId=112454) 进行远程访问。  
  
## <a name="example"></a>示例  
 下面的示例显示如何使用 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 值对插入的 FILESTREAM BLOB 执行部分更新。  
  
> [!NOTE]  
>  本示例需要在 [创建启用 FILESTREAM 的数据库](create-a-filestream-enabled-database.md) 和 [创建表以存储 FILESTREAM 数据](create-a-table-for-storing-filestream-data.md)中创建的启用了 FILESTREAM 的数据库和表。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>请参阅  
 [使用 OpenSqlFilestream 访问 FILESTREAM 数据](access-filestream-data-with-opensqlfilestream.md)   
 [为 FILESTREAM 数据创建客户端应用程序](create-client-applications-for-filestream-data.md)  
  
  
