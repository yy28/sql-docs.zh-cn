---
title: 配置和管理搜索筛选器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ccafb0bccab01286534a0c5499fe474da1262d5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027639"
---
# <a name="configure-and-manage-filters-for-search"></a>配置和管理搜索筛选器
  索引中的文档`varbinary`， `varbinary(max)`， `image`，或`xml`数据类型列需要额外的处理。 该处理必须由筛选器执行。 筛选器从文档中提取文本信息（去除格式）。 然后，筛选器将这些文本发送至与表列相关联的语言的断字器组件。  
  
 给定筛选器特定于给定文档类型（.doc、.pdf、.xls、.xml 等等）。 这些筛选器实现 IFilter 接口。 有关这些文档类型的详细信息，请查询 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) 目录视图。  
  
 二进制文档可以存储在单个 `varbinary(max)` 或 `image` 列中。 对于每个文档， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 根据文件扩展名来选择正确的筛选器。 因为文件扩展名不可见时的文件存储在`varbinary(max)`或`image`必须存储在一个单独的列在表中，称为类型列的列，文件扩展名 （.doc、.xls、.pdf 等）。 此类型列可以是任意基于字符的数据类型，并且包含文档文件扩展名，例如 .doc 表示 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word 文档。 在**文档**表中[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]、**文档**列的类型是`varbinary(max)`，而类型列中， **FileExtension**，属于类型`nvarchar(8)`。  
  
> [!NOTE]  
>  筛选器有可能能够处理嵌入到父对象中的对象，具体取决于筛选器的实现方式。 不过， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会将筛选器配置为跟踪指向其他对象的链接。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装它自己的 XML 和 HTML 筛选器。 此外，已在操作系统上安装的任何针对 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 专有格式（.doc、.xdoc、.ppt 等）的筛选器也由  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加载。 若要标识当前加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例上的筛选器，请使用 [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) 存储过程，如下所示：  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 但是，在您可以使用针对非 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 格式的筛选器之前，您必须将它们手动加载到服务器实例中。 有关安装其他筛选器的信息，请参阅 [查看或更改注册的筛选器和断字符](view-or-change-registered-filters-and-word-breakers.md)。  
  
 **查看现有全文索引中的类型列**  
  
-   [sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [FILESTREAM 与其他 SQL Server 功能的兼容性](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
