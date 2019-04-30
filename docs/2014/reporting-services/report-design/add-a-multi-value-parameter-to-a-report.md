---
title: 将多值参数添加到报表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 12ad0e77-4c28-4bbb-ab11-473ae89ec9f1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e974ab95f2e4ad5543a33f37af168a5f3b870eb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206830"
---
# <a name="add-a-multi-value-parameter-to-a-report"></a>将多值参数添加到报表
  可以将参数添加到报表，以允许用户为参数选择多个值。  
  
 您可以在报表 URL 中将多个参数值传递给报表。 有关包含多值参数的 URL 示例，请参阅 [在 URL 内传递报表参数](../pass-a-report-parameter-within-a-url.md)。  
  
 有关如何将多个参数值传递给存储过程的信息，请参阅 mssqltips.com 上的 [使用 SSRS 报表的多选参数](https://go.microsoft.com/fwlink/?LinkId=321529) 。  
  
### <a name="to-add-a-multi-value-parameter"></a>添加多值参数  
  
1.  在报表生成器中，打开您希望将多值参数添加到其中的报表。  
  
2.  右键单击报表数据集，然后单击“数据集属性”  
  
3.  通过在 **“查询”** 框中编辑查询文本或通过使用查询设计器添加筛选器，将变量添加到数据集查询中。 有关详细信息，请参阅[在关系查询设计器中生成查询（报表生成器和 SSRS）](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)。  
  
    > [!IMPORTANT]  
    >  查询文本不得包含针对查询变量的 DECLARE 语句。  
  
    > [!IMPORTANT]  
    >  查询变量的文本必须包含 `IN` 运算符，如以下示例所示。  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  如果不包含在变量两侧括号，如上所示，报表将无法呈现并会显示"必须声明标量变量"错误。  
  
     自动为查询变量创建嵌入数据集或共享数据集的数据集参数。 自动为数据集参数创建报表参数。  
  
4.  在“报表数据”窗格中展开“参数”节点，右键单击为数据集参数自动创建的报表参数，然后单击“参数属性”。  
  
5.  在 **“常规”** 选项卡中，选择 **“允许多个值”** 以允许用户为参数选择多个值。  
  
6.  （可选）在“可用”值选项卡中，指定要显示给用户的可用值列表。  
  
     可用值列表将限制用户只能选择参数的有效值。 对于多值参数，列表的顶部具有一个 **“全选”** 功能，因此用户只需一次单击即可选中或取消选中所有值。 如果您选择从数据集查询中获取报表参数的可用值，请确保选择不包含与同一报表参数关联的查询变量的数据集。  
  
     有关详细信息，请参阅[为报表参数添加、更改或删除可用值（报表生成器和 SSRS）](add-change-or-delete-available-values-for-a-report-parameter.md)。  
  
### <a name="to-add-a-multi-value-parameter"></a>添加多值参数  
  
1.  在报表生成器中，打开您希望将多值参数添加到其中的报表。  
  
2.  右键单击报表数据集，然后单击“数据集属性”  
  
3.  通过在 **“查询”** 框中编辑查询文本或通过使用查询设计器添加筛选器，将变量添加到数据集查询中。 有关详细信息，请参阅[在关系查询设计器中生成查询（报表生成器和 SSRS）](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)。  
  
    > [!IMPORTANT]  
    >  查询文本不得包含针对查询变量的 DECLARE 语句。  
  
    > [!IMPORTANT]  
    >  查询变量的文本必须包含 `IN` 运算符，如以下示例所示。  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  如果不包含在变量两侧括号，如上所示，报表将无法呈现并会显示"必须声明标量变量"错误。  
  
     自动为查询变量创建嵌入数据集或共享数据集的数据集参数。 自动为数据集参数创建报表参数。  
  
4.  在“报表数据”窗格中展开“参数”节点，右键单击为数据集参数自动创建的报表参数，然后单击“参数属性”。  
  
5.  在 **“常规”** 选项卡中，选择 **“允许多个值”** 以允许用户为参数选择多个值。  
  
6.  （可选）在“可用”值选项卡中，指定要显示给用户的可用值列表。  
  
     可用值列表将限制用户只能选择参数的有效值。 对于多值参数，列表的顶部具有一个 **“全选”** 功能，因此用户只需一次单击即可选中或取消选中所有值。 如果您选择从数据集查询中获取报表参数的可用值，请确保选择不包含与同一报表参数关联的查询变量的数据集。  
  
     有关详细信息，请参阅[为报表参数添加、更改或删除可用值（报表生成器和 SSRS）](add-change-or-delete-available-values-for-a-report-parameter.md)。  
  
## <a name="see-also"></a>请参阅  
 [向报表添加级联参数（报表生成器和 SSRS）](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [添加、更改或删除报表参数（报表生成器和 SSRS）](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  
