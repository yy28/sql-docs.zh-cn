---
title: "添加或编辑联接 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.addeditjoin.f1
ms.assetid: 3b546560-720f-48b8-9d63-cf159290e9d4
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 70780bc8284ad454014f2b1e0188d9a22db6ba03
ms.lasthandoff: 04/11/2017

---
# <a name="add-or-edit-join"></a>添加或编辑联接
  可以使用 **“添加联接”** 和 **“编辑联接”** 对话框为合并发布添加和编辑联接筛选器。  
  
> [!NOTE]  
>  编辑现有发布中的筛选器需要为该发布创建新的快照。 如果发布有订阅，则必须重新初始化这些订阅。 有关属性更改的详细信息，请参阅[更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 联接筛选器允许根据发布中相关表的筛选方式对表进行筛选。 通常，使用参数化行筛选器筛选父表；然后按照定义表之间联接的同样方式定义一个或多个联接筛选器。 联接筛选器会扩展行筛选器，以便仅在相关表中的数据与联接筛选子句匹配时才复制该数据。  
  
 联接筛选器通常遵循为其应用到的表定义的主键/外键关系，但并不严格受限于主键/外键关系。 联接筛选器可基于用于比较两个项目表中相关数据的任何逻辑。  
  
> [!IMPORTANT]  
>  联接筛选器可关联的表数量不受限制，但有大量表的筛选器会影响合并处理过程中的性能。 如果要生成五个或更多表的联接筛选器，请考虑其他解决方案：不筛选小表、不会发生更改的表或主要是查找表的表。 仅在必须跨订阅服务器分区的表之间使用联接筛选器。  
  
## <a name="options"></a>选项  
 此对话框涉及三个步骤，用以在两个表之间创建联接筛选器。 创建一个以上的联接筛选器需要多次调用此对话框。  
  
1.  **验证筛选的表并选择联接的表**  
  
    -   如果要添加新的联接，请验证 **“筛选的表”** 文本框中的表是否正确（如果不正确，请单击 **“取消”**，在 **“筛选表行”** 页中选择正确的表，并单击 **“添加联接”** 返回此对话框）。 再从 **“联接的表”** 下拉列表框中选择一个表。  
  
    -   如果正在编辑现有的联接，那么表名已经指定，无法更改。 若要更改联接所涉及的表，您必须在 **“筛选表行”** 页中删除现有联接筛选器，并在不同表之间创建新的联接。  
  
2.  **创建联接语句**  
  
    -   如果要添加新的联接，则可以选择 **“使用生成器创建语句”** 或者 **“手动编写联接语句”**。 如果您开始手动编写联接，那么将无法使用生成器。  
  
         如果选择使用生成器，请使用网格中的列（**“连接”**、 **“筛选的表列”**、 **“运算符”**、和 **“联接的表列”**）生成联接语句。 网格中的每个列都包含下拉列表框，允许你选择两个列和一个运算符（**=**、 **<>**、 **<=**、 **\<**、 **>=**、 **>**、 **like**）。 结果显示在 **“预览”** 文本区域中。 如果联接涉及不止一对列，请从**“连接”** 列中选择一个连接（ **AND**或 **OR** ），再输入另外两列和一个运算符。  
  
         如果选择手动编写语句，那么请在 **“联接语句”** 文本区域编写联接语句。 使用 **“筛选的表列”** 列表框和 **“联接的表列”** 列表框将列拖放到 **“联接语句”** 文本区域。  
  
    -   如果要编辑现有的联接，则必须手动进行编辑。  
  
3.  **指定联接选项**  
  
    -   如果在筛选的表中要联接的列是唯一的，请选择 **“唯一键”**。 对于唯一列，在合并过程中还可以使用一些专门的性能优化选项。  
  
        > [!CAUTION]  
        >  选择此选项表示联接筛选器中子表和父表是一对一还是一对多的关系。 如果父表中要联接的列具有保证唯一性的约束，才选择此选项。 如果未能正确设置此选项，可能无法收敛数据。  
  
    -   仅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本。 默认情况下，合并复制在同步过程中会逐行处理更改。 若要按单位处理相关更改，请选择 **“逻辑记录”**。 只有满足使用逻辑记录的项目和发布要求，此选项才可用。 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)中的“使用逻辑记录的注意事项”部分。  
  
 在添加或编辑完筛选器后，请单击 **“确定”** 以保存更改并关闭该对话框。 将对照 SELECT 子句中的表分析并运行指定的筛选器。 如果筛选语句有语法错误或其他问题，将会通知您编辑该筛选语句。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)   
 [联接筛选器](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
