---
title: sys. dm_filestream_file_io_handles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_filestream_file_io_handles
- sys.dm_filestream_file_io_handles
- dm_filestream_file_io_handles_TSQL
- sys.dm_filestream_file_io_handles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_handle catalog view
ms.assetid: e59632f4-3292-419f-9217-ca375749f1a5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0dd71c3d191728b04e2311017d1e446ebecaf6db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734607"
---
# <a name="sysdm_filestream_file_io_handles-transact-sql"></a>sys.dm_filestream_file_io_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  显示命名空间所有者 (NSO) 已知的文件句柄。 此视图显示了使用**OpenSqlFilestream**获取的客户端的 Filestream 句柄。  
  
|列|类型|描述|  
|------------|----------|-----------------|  
|**handle_context_address**|**varbinary(8)**|显示与客户端的句柄关联的内部 NSO 结构的地址。 可以为 Null。|  
|**creation_request_id**|**int**|显示来自 REQ_PRE_CREATE I/O 请求的用于创建此句柄的字段。 不可为 null。|  
|**creation_irp_id**|**int**|显示来自 REQ_PRE_CREATE I/O 请求的用于创建此句柄的字段。 不可为 Null。|  
|**handle_id**|**int**|显示驱动程序分配给此句柄的唯一 ID。 不可为 null。|  
|**creation_client_thread_id**|**varbinary(8)**|显示来自 REQ_PRE_CREATE I/O 请求的用于创建此句柄的字段。 可以为 Null。|  
|**creation_client_process_id**|**varbinary(8)**|显示来自 REQ_PRE_CREATE I/O 请求的用于创建此句柄的字段。 可以为 Null。|  
|**filestream_transaction_id**|**varbinary(128)**|显示与给定句柄相关联的事务的 ID。 这是**get_filestream_transaction_context**函数返回的值。 使用此字段可以联接到**sys.databases. dm_filestream_file_io_requests**视图。 可以为 Null。|  
|**access_type**|**nvarchar(60)**|不可为 null。|  
|**logical_path**|**nvarchar(256)**|显示此句柄打开的文件的逻辑路径名。 这与返回的路径相同 **。** **Varbinary**（**Max**） filestream 的 PathName 方法。 可以为 Null。|  
|**physical_path**|**nvarchar(256)**|显示文件的实际 NTFS 路径名。 这与返回的路径相同 **。** **Varbinary**（**Max**） filestream 的 .physicalpathname 方法。 它由跟踪标志 5556 启用。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [Filestream 和 FileTable 动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
