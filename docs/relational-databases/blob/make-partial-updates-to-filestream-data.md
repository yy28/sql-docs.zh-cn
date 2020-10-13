---
title: 对 FILESTREAM 数据进行部分更新 | Microsoft Docs
description: 了解如何使用 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 值对 FILESTREAM BLOB 数据进行部分更新。 查看部分更新的示例。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3b47cdacd079bfa1235427938b3fa214a1babeb7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809893"
---
# <a name="make-partial-updates-to-filestream-data"></a>对 FILESTREAM 数据进行部分更新
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  应用程序使用 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 对 FILESTREAM BLOB 数据进行部分更新。 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数将此值和从 [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 返回的句柄传递到 FILESTREAM 驱动程序。 然后，该驱动程序将当前的 FILESTREAM 数据从服务器端强制复制到该句柄所引用的文件。 如果应用程序在已写入句柄后发出 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 值，则保留最后一个写入操作，但之前对该句柄执行的写入操作将丢失。  
  
> [!NOTE]  
>  FILESTREAM 依赖于 [SMB 协议](/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview) 进行远程访问。  
  
## <a name="example"></a>示例  
 下面的示例显示如何使用 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 值对插入的 FILESTREAM BLOB 执行部分更新。  
  
> [!NOTE]  
>  本示例需要在 [创建启用 FILESTREAM 的数据库](../../relational-databases/blob/create-a-filestream-enabled-database.md) 和 [创建表以存储 FILESTREAM 数据](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)中创建的启用了 FILESTREAM 的数据库和表。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 OpenSqlFilestream 访问 FILESTREAM 数据](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [为 FILESTREAM 数据创建客户端应用程序](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
