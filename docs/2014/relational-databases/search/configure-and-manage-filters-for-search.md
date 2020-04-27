---
title: 配置和管理搜索筛选器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: df228060a5b714d92c9ae200d91851e4b579839d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011583"
---
# <a name="configure-and-manage-filters-for-search"></a>配置和管理搜索筛选器
  为 `varbinary`、`varbinary(max)`、`image` 或 `xml` 数据类型的文档建立索引需要进行额外处理。 该处理必须由筛选器执行。 筛选器从文档中提取文本信息（去除格式）。 然后，筛选器将这些文本发送至与表列相关联的语言的断字器组件。  
  
 给定筛选器特定于给定文档类型（.doc、.pdf、.xls、.xml 等等）。 这些筛选器实现 IFilter 接口。 有关这些文档类型的详细信息，请查询 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) 目录视图。  
  
 二进制文档可以存储在单个 `varbinary(max)` 或 `image` 列中。 对于每个文档， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 根据文件扩展名来选择正确的筛选器。 由于文件存储在`varbinary(max)`或`image`列中时，文件扩展名不可见，因此文件扩展名（.doc、.xls、.pdf 等）必须存储在表中单独的列中，称为类型列。 此类型列可以是任意基于字符的数据类型，并且包含文档文件扩展名，例如 .doc 表示 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word 文档。 在的**document**表中[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]， **document**列的类型`varbinary(max)`为，类型列**FileExtension**的类型为`nvarchar(8)`。  
  
> [!NOTE]  
>  筛选器有可能能够处理嵌入到父对象中的对象，具体取决于筛选器的实现方式。 不过， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会将筛选器配置为跟踪指向其他对象的链接。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装它自己的 XML 和 HTML 筛选器。 此外，已在操作系统上安装的任何针对 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 专有格式（.doc、.xdoc、.ppt 等）的筛选器也由  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加载。 若要标识当前加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例上的筛选器，请使用 [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) 存储过程，如下所示：  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 但是，在您可以使用针对非 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 格式的筛选器之前，您必须将它们手动加载到服务器实例中。 有关安装其他筛选器的信息，请参阅 [查看或更改注册的筛选器和断字符](view-or-change-registered-filters-and-word-breakers.md)。  
  
 **查看现有全文索引中的类型列**  
  
-   [sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>另请参阅  
 [sys. fulltext_index_columns &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [FILESTREAM 与其他 SQL Server 功能的兼容性](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
