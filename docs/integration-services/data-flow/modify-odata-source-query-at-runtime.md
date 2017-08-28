---
title: "提供在运行时的 OData 源查询 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>提供在运行时的 OData 源查询
 你可以通过添加修改在运行时的 OData 源查询*表达式*到**[OData Source]。 [查询]**数据流任务的属性。  
  
 返回的列一定要在设计时; 返回的相同列否则，执行包时收到错误。 请务必在使用 $select 查询选项时指定相同的列（采用相同顺序）。 使用 $select 选项的更安全替代方法是直接从源组件 UI 中取消选择不需要的列。  
  
 可通过几种不同的方式在运行时动态设置查询值。 以下是一些较常用的方法。  
  
## <a name="provide-the-query-as-a-parameter"></a>作为参数提供查询  
 以下过程演示如何公开 OData 源组件用作包的参数的查询。  
  
1.  右键单击 **“数据流任务”** 并选择 **“参数化…”** 选项。  
  
2.  在**参数化**对话框中，选择**[\<的 OData 源组件的名称 >]。 [查询]**为**属性**。  
  
3.  选择是 **“创建新参数”** 还是 **“使用现有参数”**。  
  
4.  如果你选择**创建新参数**:  
  
    1.  为参数输入 **“名称”** 和 **“说明”** 。  
  
    2.  为参数指定默认 **“值”** 。  
  
    3.  为参数指定“范围”（“包”或“项目”）。  
  
    4.  指定参数是否为 **“必需”**  
  
5.  单击 **“确定”** 关闭对话框。  
  
## <a name="provide-the-query-with-an-expression"></a>使用的表达式提供查询
 当你想要动态构造查询字符串在运行时，此方法很有用。
  
1.  选择**数据流任务**，其中包含你**OData 源**。  
  
2.  在 **“属性”** 窗口中，突出显示 **“表达式”** 属性。  
  
3.  单击 ... （省略号） 按钮以打开**属性表达式编辑器**。  
  
4.  选择“[OData 源].[查询]”属性。  
  
5.  单击 ... （省略号） 按钮**表达式**。  
  
6.  输入 **“表达式”**。  
  
7.  单击 **“确定”**。  
  
> [!NOTE]  
> 当你使用此方法时，你必须确保你设置的值正确进行 URL 编码。 从用户输入接收值时（例如，通过参数设置各个查询选项值），必须确保值已验证，以避免潜在的 SQL 注入类型攻击。  
  
  
