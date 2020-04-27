---
title: 在运行时修改 OData 源查询 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1fac598789c53f460ed5239f304de2a39acff81
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62901184"
---
# <a name="modify-odata-source-query-at-runtime"></a>在运行时修改 OData 源查询
  可以通过向数据流任务的“[OData 源].[查询]”**** 属性添加表达式，在运行时修改 OData 源查询。  
  
 请注意，列必须保持与设计时使用的内容相同；否则执行包时会出现错误。 请务必在使用 $select 查询选项时指定相同的列（采用相同顺序）。 使用 $select 选项的更安全替代方法是直接从源组件 UI 中取消选择不需要的列。  
  
 可通过几种不同的方式在运行时动态设置查询值。 下面是一些较常用的方法。  
  
## <a name="exposing-the-query-as-a-parameter"></a>将查询公开为参数  
 以下过程包含的步骤可将 OData 源组件使用的查询公开为包的参数。  
  
1.  右键单击“数据流任务”并选择“参数化…”选项   。  
  
2.  在“参数化”对话框中，针对“属性”选择“[**OData 源组件的名称>].[查询]”** **\<**  。  
  
3.  选择是 **“创建新参数”** 还是 **“使用现有参数”** 。  
  
4.  如果选择 **“创建新参数”**，请执行以下操作：  
  
    1.  为参数输入 **“名称”** 和 **“说明”** 。  
  
    2.  为参数指定默认 **“值”** 。  
  
    3.  为参数指定“范围”  （“包”  或“项目”  ）。  
  
    4.  指定参数是否为 **“必需”**  
  
5.  单击 **“确定”** 关闭对话框。  
  
## <a name="using-an-expression"></a>使用表达式  
 当您要在运行时动态构造查询字符串时，可使用此方法。 在此示例中，MaxRows 变量将通过其他方法（脚本、参数等）进行设置。  
  
1.  选择包含 **“OData 源”** 的 **“数据流任务”**。  
  
2.  在 **“属性”** 窗口中，突出显示 **“表达式”** 属性。  
  
3.  单击 .。。（省略号）按钮以显示 "**属性表达式编辑器**"。  
  
4.  选择“[OData 源].[查询]”**** 属性。  
  
5.  单击 .。。**表达式**的 "（省略号）" 按钮。  
  
6.  输入**表达式**。  
  
7.  单击" **确定**"。  
  
> [!WARNING]  
>  请注意，当使用此方法时，需要确保设置的值为正确编码的 URL。 从用户输入接收值时（例如，通过参数设置各个查询选项值），必须确保值已验证，以避免潜在的 SQL 注入类型攻击。  
  
  
