---
title: 使用计划指南指定查询参数化行为 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da60ceee93802b14b7d09392740a1f6b471e4ab1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150607"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>使用计划指南指定查询参数化行为
  当 PARAMETERIZATION 数据库选项设置为 SIMPLE 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器可以选择参数化查询。 这意味着查询中包含的任何文字值都用参数来替换。 此过程称为简单参数化。 SIMPLE 参数化生效后，将无法控制参数化哪些查询，不参数化哪些查询。 不过，您可以通过将 PARAMETERIZATION 数据库选项设置为 FORCED 来指定参数化数据库中的所有查询。 此过程称为强制参数化。  
  
 可以通过下列方式使用计划指南来覆盖数据库的参数化行为：  
  
-   当 PARAMETERIZATION 数据库选项设置为 SIMPLE 时，您可以指定对某一类查询尝试执行强制参数化。 可以通过在查询的参数化表单上创建 TEMPLATE 计划指南并在 [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) 存储过程中指定 PARAMETERIZATION FORCED 查询提示来完成此操作。 您可以将此种计划指南看作只对某一类查询（而不是所有查询）启用强制参数化的方法。  
  
-   当 PARAMETERIZATION 数据库选项设置为 FORCED 时，您可以指定对某一类查询仅尝试执行简单参数化而非强制参数化。 可以通过在查询的强制参数化表单上创建 TEMPLATE 计划指南并在 **sp_create_plan_guide**中指定 PARAMETERIZATION SIMPLE 查询提示来完成此操作。  
  
 请考虑 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的以下查询：  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 作为数据库管理员，您已确定不想对数据库中的所有查询启用强制参数化。 不过，您确实想避免所有语法上与前一个查询相同而只是常量文字值不同的查询的编译开销。 换句话说，您想参数化该查询，使此种查询的查询计划可以再次使用。 在此情况下，请完成下列步骤：  
  
1.  检索查询的参数化表单。 获取此值以用于 **sp_create_plan_guide** 的唯一安全方法是使用 [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) 系统存储过程。  
  
2.  请指定 PARAMETERIZATION FORCED 查询提示以对查询的参数化表单创建计划指南。  
  
    > [!IMPORTANT]  
    >  作为参数化查询的一部分， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根据文字的值和大小，将数据类型分配给替换文字值的参数。 对于传递给**@stmt** **sp_get_query_template**的 output 参数的常量文本值，将发生相同的过程。 由于在**@params** **sp_create_plan_guide**的参数中指定的数据类型必须与参数的参数化查询的数据类型匹配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因此您可能需要创建多个计划指南以涵盖查询的可能参数值的完整范围。  
  
 以下脚本既可用于获取参数化查询也可用于之后对其创建计划指南：  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 同样，在已启用强制参数化的数据库中，可以确保按照简单参数化规则对示例查询以及其他语法相同但常量文字值不同的查询进行参数化。 若要实现此目的，请在 OPTION 子句中指定 PARAMETERIZATION SIMPLE 而不指定 PARAMETERIZATION FORCED。  
  
> [!NOTE]  
>  TEMPLATE 计划指南使语句与在仅包含单个语句的批处理中提交的查询匹配。 多语句批处理中的语句通过 TEMPLATE 计划指南进行匹配是不合格的。  
  
  
