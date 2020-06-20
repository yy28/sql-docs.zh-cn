---
title: 演练：添加和更改数据库关系图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: c7314598bffe53b6db1c24ecaaec2cf32ee06cb7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008598"
---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>演练：添加和更改数据库关系图
  本演练说明了如何创建和修改数据库关系图以及如何通过数据库关系图组件更改数据库。 您将看到如何向关系图添加表、如何创建表之间的关系、如何对列创建约束和索引以及如何更改每个表的信息级别。  
  
## <a name="prerequisites"></a>必备条件  
 为了完成本演练，您需要：  
  
-   能够访问带有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示例数据库的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]  
  
-   一个具有数据库所有者 `dbo` 特权的帐户  
  
> [!NOTE]  
>  如果所使用的帐户对要更改的表不具有足够的特权，则在尝试更改表时会出现错误消息。  
  
## <a name="creating-a-diagram"></a>创建关系图  
  
#### <a name="to-create-a-new-database-diagram"></a>创建新的数据库关系图  
  
1.  在“视图”  菜单上单击“对象资源管理器”  。  
  
2.  打开“数据库”节点，再打开 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 节点。  
  
3.  右键单击“数据库关系图”节点并选择“新建数据库关系图”  。  
  
     如果此数据库没有创建关系图所必需的对象，则将显示下列消息： **此数据库没有使用数据库关系图创建功能所需的一个或多个支持对象。要创建它们吗？** 选择“是”  。  
  
     此时将显示“添加表”  对话框。  
  
4.  选择“AddressType (Person)”  和“Address (Person)”  并单击“添加”  。  
  
     两个表将添加到关系图中。  
  
5.  关闭“添加表”  对话框。  
  
#### <a name="to-view-different-column-data"></a>查看不同的列数据  
  
1.  右键单击 `Address` 表。 在快捷菜单上，指向“表视图”  ，再单击“标准”  。  
  
     表的网格将显示三个列：“列名”  、“数据类型”  和“允许 Null 值”  。  
  
2.  右键单击 `Address` 表，单击“表视图”  并选择“键”  。  
  
     表网格将显示一个列，并带有表列名。 仅显示那些参与了索引的列。  
  
## <a name="creating-new-tables"></a>创建新表  
  
#### <a name="to-create-tables-within-diagram-designer"></a>在关系图设计器中创建表  
  
1.  右键单击现有表外部的关系图设计器并选择“新建表”  。  
  
2.  在 "**选择名称**" 对话框中，单击 **"确定"** 以接受默认名称 `Table1` 。  
  
     将显示具有以下三列的新表网格：“列名”  、“数据类型”  和“允许 Null 值”  。  
  
3.  将以下信息添加到 `Table1` ：  
  
    |**列名称**|**数据类型**|**允许 Null 值**|  
    |---------------------|-------------------|---------------------|  
    |`T1col1`|`int`|checked|  
    |`T1col2`|`varchar(50)`|checked|  
    |`T1col3`|`float`|已选中|  
  
4.  右键单击 `T1col1` 并选择“设置主键”****。  
  
     列名旁将显示一个钥匙图标。  
  
5.  从“文件”**** 菜单，单击“保存 Diagram1”****。  
  
6.  在 "**选择名称**" 对话框中，单击 **"确定"** 以接受默认名称 `Diagram1` 。  
  
7.  将显示“保存”**** 对话框和一条指出 `Table1` 将保存到数据库的消息。 单击 **“是”** 。  
  
## <a name="modifying-table-structure"></a>修改表结构  
 您可以添加检查约束，并在关系图设计器中建立表之间的关系。  
  
#### <a name="to-create-check-constraints"></a>创建检查约束  
  
1.  在 `Table1` 中，右键单击 `T1col3` 行并选择“CHECK 约束”****。  
  
     此时将显示“CHECK 约束”**** 对话框。  
  
2.  单击“添加”。  
  
     “选定的 CHECK 约束”**** 列表中将出现一个新约束，默认名称为 `CK_Table1`。  
  
3.  在网格中选择“表达式”**** 行并单击省略号按钮。  
  
     此时将显示“CHECK 约束表达式”**** 对话框。  
  
4.  键入 `T1col3 > 5` ，然后单击 **“确定”**。  
  
     `Table1` 现在有了一个约束，即输入到 `T1col3` 中的所有值都必须大于 5。  
  
5.  单击“关闭” 。  
  
#### <a name="to-create-relationships-between-tables"></a>在表之间创建关系  
  
1.  在关系图设计器中创建名为 `Table2` 的新表，该表具有以下列：  
  
    |**列名**|**数据类型**|**允许 Null 值**|  
    |---------------------|-------------------|---------------------|  
    |`T2col1`|`int`|未选中|  
    |`T2col2`|`varchar(50)`|checked|  
    |`T2col3`|`xml`|checked|  
  
    > [!NOTE]  
    >  外键关系的主键方上的列必须参与主键或唯一约束。  
  
2.  将 `T2col1` 拖动到 `T1col1`。  
  
     将显示两个对话框：背景中的“外键关系”**** 对话框和前景中的“表和列”**** 对话框。  
  
3.  单击“确定”**** 保存新的关系。  
  
4.  再单击“确定”****。  
  
## <a name="creating-indexes"></a>创建索引  
 您可以对大多数数据类型（包括 XML）创建索引。  
  
#### <a name="to-create-a-standard-index"></a>创建标准索引  
  
1.  右键单击 `Table1` 并选择“索引/键”****。  
  
     此时将显示“索引/键”**** 对话框。  
  
2.  单击“添加”。  
  
     “选定的主/唯一键或索引”**** 列表中将出现一个新索引，并使用类似 `IX_Table1` 的默认名称。  
  
3.  选择“列”**** 行并单击省略号按钮。  
  
     此时将显示“索引列”**** 对话框。  
  
4.  单击“列名”**** 下方的下拉箭头并选择 `T1col2`。  
  
    > [!NOTE]  
    >  您可以通过选择 `T1col2` 下的单元并选择其他列名来向此索引添加其他列。  
  
5.  单击“确定”**** 保存此索引。  
  
6.  在“索引/键”**** 对话框中单击“关闭”****。  
  
#### <a name="to-create-an-xml-index"></a>创建 XML 索引  
  
1.  右键单击 `T2col1` 并选择“设置主键”****。  
  
    > [!NOTE]  
    >  添加 XML 索引要求将表中的另一列设置为聚集主键。  
  
2.  在 `T2col3` 中右键单击 `Table2` 行，并选择“XML 索引”****。  
  
     此时将显示“XML 索引”**** 对话框。  
  
3.  单击“添加”。  
  
     将向“选定的 XML 索引”**** 列表中添加一个具有默认值的 XML 索引。  
  
4.  单击“关闭” 。  
  
    > [!NOTE]  
    >  XML 索引是按列创建的。 第一个 XML 索引是主索引，所有其他索引都是辅助索引。  
  
## <a name="saving-the-diagram"></a>保存关系图  
 对关系图所做的全部更改在保存后才会发布到数据库。 如果存在问题或冲突，则会出现一个带有详细信息的对话框。  
  
#### <a name="to-save-a-database-diagram"></a>保存数据库关系图  
  
1.  在“文件”**** 菜单上，选择“保存 Diagram1”****。  
  
     此时将显示“保存”**** 对话框。 如果选中了“表受到影响时警告”****，则会列出有关新表或更改的表的信息。  
  
2.  单击“确定”。  
  
3.  如果发生了任何错误，则会出现“保存后的通知”**** 对话框，显示错误及其原因。 修复错误并再次保存关系图。  
  
## <a name="next-steps"></a>后续步骤  
 虽然这是一个仅包含两个现有表和两个新表的简单关系图，但是它展示了创建现有数据库的关系图或直观地创建新架构的潜力。 建议了解的其他内容包括：  
  
-   创建包含多组相关表的新关系图  
  
-   自定义各表中显示的信息量  
  
-   更改布局和添加批注  
  
-   将关系图复制到位图  
  
## <a name="see-also"></a>另请参阅  
 [自定义关系图中显示的信息量 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [&#40;Visual Database Tools 设置数据库关系图设计器&#41;](set-up-database-diagram-designer-visual-database-tools.md)   
 [在 Visual Database Tools &#40;向关系图中添加表&#41;](add-tables-to-diagrams-visual-database-tools.md)   
 [在 Visual Database Tools&#41;的关系图上创建表之间的关系 &#40;](create-relationships-between-tables-on-a-diagram-visual-database-tools.md)   
 [创建 XML 索引](../../relational-databases/xml/create-xml-indexes.md)   
 [将数据库关系图的图像复制到剪贴板 &#40;Visual Database Tools&#41;](copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)   
 [使用关系图布局 (Visual Database Tools)](work-with-diagram-layout-visual-database-tools.md)  
  
  
