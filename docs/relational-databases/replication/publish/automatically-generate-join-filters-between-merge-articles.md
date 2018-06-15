---
title: 在合并项目之间自动生成联接筛选器 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fc107aab8433822e5d674b39b8b4986ec32f4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32963012"
---
# <a name="automatically-generate-join-filters-between-merge-articles"></a>在合并项目之间自动生成联接筛选器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在新建发布向导的“筛选表行”页上，或在“发布属性 - \<发布>”对话框的“筛选行”页上自动生成一组联接筛选器。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)和[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
> [!NOTE]  
>  如果你在发布订阅初始化后在“发布属性 - \<发布>”对话框中自动生成一组联接筛选器，则必须生成一个新快照，并在进行更改后重新初始化所有订阅。 有关属性更改要求的详细信息，请参阅[更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 可以手动为一组表创建联接筛选器，也可由复制根据表上定义的外键和主键的关系自动生成联接筛选器。 有关手动创建联接筛选器的详细信息，请参阅[定义和修改合并项目间的联接筛选器](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>在合并项目之间自动生成一组联接筛选器  
  
1.  在新建发布向导的“筛选表行”页上，或在“发布属性 - \<发布>”的“筛选行”页上，依次单击“添加”和“自动生成筛选器”。  
  
    > [!NOTE]  
    >  自动生成筛选器将删除发布中所有现有的行筛选器或联接筛选器。 可以在自动生成一组筛选器后添加筛选器。  
  
2.  按照 **“生成筛选器”** 对话框中的过程创建行筛选器。 然后通过主键和外键的关系将行筛选器扩展到与筛选的表有关的表。  
  
    1.  从下拉列表框中选择要筛选的表。  
  
    2.  在 **“筛选语句”** 文本框中创建一个筛选语句。 您可以在文本区域中直接键入，也可以从 **“列”** 列表框中拖放列。  
  
         **“筛选语句”** 文本区域包括默认的文本，其格式为：  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         不能更改默认文本；在 WHERE 关键字后使用标准的 SQL 语法键入静态行筛选器或参数化行筛选器的筛选器子句。 参数化行筛选器的完整筛选器子句如下所示：  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 子句应使用由两部分构成的命名方式，不支持由三部分和四部分构成的命名方式。  
  
    3.  指定筛选选项。  
  
         选择与订阅服务器之间共享数据的方式相匹配的选项： **“此表中的行将转到多个订阅”** 或 **“此表中的行将仅转到一个订阅”**。 如果选择 **“此表中的行将仅转到一个订阅”**，则合并复制可以通过存储和处理较少的元数据来优化性能。 但是，必须确保在对数据分区时不能将行复制到多个订阅服务器。 有关详细信息，请参阅主题 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)中的“设置‘分区选项’”部分。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     将对照 SELECT 子句中的表分析并运行指定的筛选器。 如果筛选语句有语法错误或其他问题，将会通知您编辑该筛选语句。  
  
     分析语句后，复制将创建必需的联接筛选器，并在 **“筛选表行”** 页或 **“筛选行”** 页的 **“筛选的表”** 窗格中显示这些联接筛选器。 如果从新建发布向导生成筛选器，并且尚未为运行此向导的发布服务器配置分发服务器，系统会提示您进行此项配置。  
  
4.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>修改自动生成的筛选器  
  
1.  在新建发布向导的“筛选表行”页或“发布属性 - \<发布>”的“筛选行”页上，在“筛选的表”窗格中选择筛选器，然后单击“编辑”。  
  
2.  在 **“编辑筛选器”** 或 **“编辑联接”** 对话框中修改筛选器。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>删除自动生成的筛选器  
  
1.  在新建发布向导的“筛选表行”页或“发布属性 - \<发布>”的“筛选行”页上，在“筛选的表”窗格中选择筛选器，然后单击“删除”。  
  
## <a name="see-also"></a>另请参阅  
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
