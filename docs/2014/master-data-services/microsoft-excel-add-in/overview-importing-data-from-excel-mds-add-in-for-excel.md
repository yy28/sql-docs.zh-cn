---
title: 发布数据 (MDS add-in for Excel) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5ed014aaed74ea9da70485b73d089e8ddaae0f43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765490"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>发布数据（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，要想与其他用户共享数据，可将数据发布到 MDS 存储库。 数据一经发布，即可供该外接程序的其他用户下载。  
  
 发布数据时，已添加或更新的所有数据都会发布到 MDS 存储库。 已删除的数据不会发布，必须单独删除数据。 有关详细信息，请参阅 [删除行（用于 Excel 的 MDS 外接程序）](delete-a-row-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  发布不能用于创建新实体。 有关创建实体的详细信息，请参阅[创建实体（用于 Excel 的 MDS 外接程序）](create-an-entity-mds-add-in-for-excel.md)。  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>当多个用户同时发布时  
 多个用户可以对相同的数据发布更新。 更新会在每个用户发布时保存到数据库中。 这表示未使用最近更新的数据的用户仍可以在自己发布时更改数据值。  
  
 只有更新的数据才会发布到数据库中。 不发布工作表中的任何过时数据。  
  
## <a name="transactions-and-annotations"></a>事务和批注  
 每个已发布的更改都保存为一个事务。 如果您愿意，则可以向事务添加批注（注释），解释您做出更改的原因。  
  
-   您不能为删除操作添加批注，尽管删除操作可另存为管理员可以撤消的事务。  
  
-   如果您更改**代码**值对于成员，它不会记录为事务，并为该成员以前所有的事务都不可用。  
  
-   您可以查看其他用户对成员执行的事务。 还可以查看对成员执行的所有事务，即便不再对特定属性拥有权限。  
  
 您可以查看对成员执行的所有事务。 有关详细信息，请参阅[查看成员的所有批注或事务（用于 Excel 的 MDS 外接程序）](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)。  
  
> [!IMPORTANT]  
>  如果您输入的批注超过 500 个字符，该批注将被自动截断。  
  
## <a name="business-rule-and-other-validation"></a>业务规则和其他验证  
 发布数据时，将执行验证，在确保数据准确无误后才将其添加到 MDS 存储库中。 如果数据不符合指定的条件，则不会将其发布到存储库。 有关详细信息，请参阅[验证数据（用于 Excel 的 MDS 外接程序）](validating-data-mds-add-in-for-excel.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|将数据从活动工作表发布回 MDS 存储库。|[数据从 Excel 发布到 MDS &#40;MDS add-in for Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|同时从 MDS 存储库和工作表中删除行。|[删除行（用于 Excel 的 MDS 外接程序）](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [刷新数据（用于 Excel 的 MDS 外接程序）](refreshing-data-mds-add-in-for-excel.md)  
  
-   [用于 Microsoft Excel 的 Master Data Services 外接程序](master-data-services-add-in-for-microsoft-excel.md)  
  
  
