---
title: 编辑表 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b048936c1312bf9c82c9d14586af3df44422a521
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921645"
---
# <a name="edit-tables"></a>编辑表

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  使用 **“表”** 选项卡可对您从 Oracle 源数据库中选择的表和列进行更改。 该选项卡具有以下元素：  
  
 **表列表**  
 此表列表具有三列：  
  
-   **Oracle 表名称**：表的名称，包括表架构。  
  
-   **捕获实例**：用于命名特定于实例的变更数据捕获对象的捕获实例的名称。 捕获实例不能为 NULL。 如果未指定，则该名称将从源架构名称加上源表名称中派生而来，格式为 `<schema-name>_<table-name>.` 。捕获实例名称不能超过 100 个字符，并且在数据库中必须是唯一的。 可单击此列的任意单元格对 **capture_instance**进行手动编辑。  
  
-   **安全角色**：用于获取对更改数据的访问权限的数据库角色的名称。 可单击此列的任意单元格对 **security_role**进行手动编辑。  
  
 **添加表**  
 单击“添加表”  可打开“表选择”对话框，从中可以[将表添加到 CDC 实例](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)。 首次访问 Oracle 数据库时，您必须 [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)。  
  
 **编辑**  
 从该列表中选择一个表，然后选择“编辑”  以便打开该表的“属性”  对话框，从中可以[编辑表格属性](../../integration-services/change-data-capture/edit-the-table-properties.md)。  
  
> [!NOTE]  
>  您不能编辑已具有镜像表的表的类型映射。 只能对新表执行此操作。  
  
 **删除**  
 从该列表中选择一个表，然后单击“删除”  可从 CDC 实例中删除该表。  
  
## <a name="see-also"></a>另请参阅  
 [如何编辑 CDC 实例属性](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [选择 Oracle 表和列](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
