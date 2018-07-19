---
title: 如何修复错误 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4984e28ae3397b6296f8d1a39a6d32474b27f9c
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093765"
---
# <a name="how-to-fix-errors"></a>如何修复错误
“错误列表”窗格显示任何部署或生成错误。 当你编辑数据库实体及其定义时，因在 Transact\-SQL 编辑器或表设计器中编辑而导致的语法和语义错误也会显示在列表中。 在您跨不同的选项卡编辑脚本时，错误列表将动态更新。 然后，您可以按照标识的错误进一步排除故障。  
  
> [!WARNING]  
> 以下过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)和[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)部分中的过程中创建的实体。  
  
### <a name="to-fix-errors"></a>修复错误  
  
1.  在“解决方案资源管理器”中，右键单击“Product”表 (Product.sql)，然后选择“视图设计器”。  
  
2.  在设计器的列网格中，右键单击 ShelflLife 列，然后选择“删除”以便从表中删除该列。  
  
3.  请注意，在屏幕底部的“错误列表”窗格中，如下警告和错误将立即弹出。  
  
**警告 SQL71502: 函数 [dbo].[GetProductsBySupplier] 包含对某一对象的无法解析的引用。** 或者该对象不存在，或者该引用不明确，因为它可能引用任何以下对象: [dbo].[Product].[p]::[ShelfLife] 或 [dbo].[Product].[ShelfLife]。错误 SQL71501: CHECK 约束: [dbo].[CK_Product_ShelfLife] 具有对对象 [dbo].[Product].[ShelfLife] 的无法解析的引用。  
  
4.  你可以右键单击“错误列表”，然后使用上下文菜单对结果进行排序、筛选要显示的条目以及希望为每个条目出现的信息列。  
  
    双击标识的第一个警告并按其访问生成了该警告的脚本文件。 有问题的代码部分将突出显示。 在此示例中，这是因为 `ShelfLife` 列正在由前面创建的表值函数中的 `RETURN` 和 `SELECT` 语句使用。  
  
5.  在 Transact\-SQL 编辑器中，从该函数中删除 `ShelfLife`。  
  
6.  通过删除检查约束，以类似的方式修复第二个错误。  
  
7.  请注意，在解决了这些问题后，警告和错误将立即从“错误列表”中消失。  
  
## <a name="see-also"></a>另请参阅  
[使用 Transact-SQL 编辑器编辑和执行脚本](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
