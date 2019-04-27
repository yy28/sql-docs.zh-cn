---
title: 搜索属性列表编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 818e1176cb5a4f81205a36dc7be6fd9fded286ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773665"
---
# <a name="search-property-list-editor"></a>搜索属性列表编辑器
  使用此对话框可以在搜索属性列表中添加或删除搜索属性。  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>使用 SQL Server Management Studio 管理搜索属性列表  
 有关如何创建、 查看或删除搜索属性列表，以及有关如何配置为属性搜索的全文索引的信息，请参阅[使用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="options"></a>选项  
 **属性名称**  
 指定要用来标识全文查询中的属性的名称。 属性名称可以包含内部空格。 **“属性名称”** 的最大长度为 256 个字符。 此名称可以是“作者”或“家庭地址”等此类用户友好名称，也可以是 Windows 的属性规范名称，如 `System.Author` 或 `System.Contact.HomeAddress`。 **“属性名称”** 必须唯一标识属性集中的属性。  
  
 开发人员使用属性名称来标识 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 谓词中的属性。 因此，当添加属性时，务必指定一个在含义上表示该属性的值。  
  
 **属性集 GUID**  
 指定属性所属的属性集的标识符。 这是全局唯一标识符 (GUID)。 属性集是一组在逻辑上相关的属性。 有关获取此值的信息，请参阅本主题后面的“备注”。  
  
 **属性 Int ID**  
 指定属性的属性整型标识符。 这一预先分配的值是一个正整数，它在属性集中是唯一的。 有关获取此值的信息，请参阅本主题后面的“备注”。  
  
> [!NOTE]  
>  全文搜索不支持使用字符串标识符的文档属性。  
  
 **属性说明**  
 指定属性的说明（可选）。 这是一个最多 512 个字符的字符串。 例如，说明可能包含有关属性的属性集的信息，或者包含有关从名称上不能直接看出其含义的属性的信息。  
  
## <a name="remarks"></a>备注  
 若要向搜索属性列表添加搜索属性，必须为此属性所属的属性集指定全局唯一标识符 (GUID)，并指定此属性的属性整型标识符。 这些标识符的给定组合在给定的搜索属性列表中必须是唯一的。 如果试图添加一个现有组合，则此操作将失败并且会发出错误。 这意味着，您只能为给定属性配置一个名称。  
  
 属性说明是可选的。  
  
 **若要配置全文索引的搜索属性列表**  
  
-   [使用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>权限  
 请参阅[ALTER SEARCH PROPERTY LIST &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [ALTER SEARCH PROPERTY LIST (Transact-SQL)](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [使用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
