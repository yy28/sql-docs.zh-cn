---
title: 选择 Oracle 表和列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4e81a1faea62b2ecadff200a7383600e604661a7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435444"
---
# <a name="select-oracle-tables-and-columns"></a>选择 Oracle 表和列
  使用“选择 Oracle 表和列”页可以从捕获了更改的 Oracle 源数据库选择表。 该页具有以下元素：  
  
## <a name="options"></a>选项  
 **表列表**  
 此表列表具有三列：  
  
-   **Oracle 表名称**：表的名称，包括表架构。  
  
-   **捕获实例**：用于命名特定于实例的变更数据捕获对象的捕获实例的名称。 捕获实例不能为 NULL。  
  
     如果未指定，则该名称将从源架构名称加上源表名称中派生而来，格式为 `<schema-name>_<table-name>`。 捕获实例名称不能超过 100 个字符，并且在数据库中必须是唯一的。  
  
     可单击此列的任意单元格对 **capture_instance**进行手动编辑。  
  
-   **安全角色**：用于控制对更改数据的访问的数据库访问控制角色的名称。  
  
     可单击此列的任意单元格对 **security_role**进行手动编辑。  
  
 **添加表**  
 单击“添加表”  可打开“表选择”对话框，从中你可以[为捕获更改选择 Oracle 表](select-oracle-tables-for-capturing-changes.md)。  
  
 **编辑**  
 从该列表中选择一个表，然后选择“编辑”  以便打开该表的“属性”  对话框，从中你可以[对为捕获更改选择的表进行更改](make-changes-to-the-tables-selected-for-capturing-changes.md)。  
  
 **删除**  
 从该列表中选择一个表，然后单击“删除”  可从 CDC 实例中删除该表。  
  
 在使用正确的对话框[为捕获更改选择 Oracle 表](select-oracle-tables-for-capturing-changes.md)或[对为捕获更改选择的表进行更改](make-changes-to-the-tables-selected-for-capturing-changes.md)后，单击“下一步”  以[生成和运行补充日志记录脚本](generate-and-run-the-supplemental-logging-script.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何创建 SQL Server 更改数据库实例](how-to-create-the-sql-server-change-database-instance.md)   
 [编辑表](edit-tables.md)   
 [将表添加到 CDC 实例](add-tables-to-a-cdc-instance.md)   
 [编辑表属性](edit-the-table-properties.md)  
  
  
