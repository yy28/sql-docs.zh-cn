---
title: 缓存的位置 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288615"
---
# <a name="location-of-cache"></a>缓存的位置
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 游标库在内存和 Windows 中缓存数据®临时文件中。 这将限制光标库只能按可用磁盘空间处理的结果集的大小。 如果插入到游标库缓存的末尾，则当要缓存的数据将跨越段边界时，将使用临时文件。 相反，要缓存的数据将添加，以代替缓存中上次保存的数据块。 上次保存的数据块保存在临时文件中。 如果游标库异常终止（例如，当电源发生故障时），它可以将 Windows 临时文件保留在磁盘上。 这些名为 _CTT*nnnn*.tmp，并在当前目录中创建。  
  
> [!NOTE]  
>  如果 Microsoft 中的游标库® WindowsNT®/Windows2000 尝试在当前目录中的临时文件中缓存数据，而应用程序从只读共享或压缩磁盘（如 Microsoft 基础类库示例）运行时，将返回 SQLSTATE HY000（无法创建文件缓冲区的一般错误）。
