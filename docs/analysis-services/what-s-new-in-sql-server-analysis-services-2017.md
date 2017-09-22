---
title: "什么 &#39; SQL Server 自 2017 年 Analysis Services 中的新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: eb98483d6237f2db2fdb0cb9aa444dd938a431f0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>什么 &#39; SQL Server 自 2017 年 Analysis Services 中的新增功能
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>SQL Server 自 2017 年分析服务 RC2
此版本中没有新增功能。 此版本中的改进包括 bug 修补程序和性能。

## <a name="sql-server-2017-analysis-services-rc1"></a>SQL Server 自 2017 年 Analysis Services RC1
在此版本中没有新功能，但是，此版本包括对其他改进[动态管理视图](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services)(DMV) 用于在 1200年和 1400年兼容性级别的表格模型。

现在 DISCOVER_CALC_DEPENDENCY 适用于表格 1200年和 1400年模型。 表格 1400年模型显示 M 分区、 M 表达式和结构化的数据源之间的依赖关系。 若要了解详细信息，请参阅[Analysis Services 博客](https://blogs.msdn.microsoft.com/analysisservices/)。

MDSCHEMA_MEASUREGROUP_DIMENSIONS 改进都包含此 DMV，各种客户端工具使用它来显示度量值维数。 例如，Excel 数据透视表中的资源管理器功能允许用户以跨钻取至与所选度量值相关的维度。 此发行版将更正基数列，其中已以前显示不正确的值。

## <a name="sql-server-analysis-services-ctp-21"></a>SQL Server Analysis Services CTP 2.1
此版本中没有新增功能。 在此版本中的改进包括 bug 修补程序和性能，并且增强功能[动态管理视图](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services)(DMV)。 DMV 是 SQL Server Profiler 中的查询，其返回有关本地服务器操作和服务器运行状况的信息。 有关更多详细信息，请参阅[Analysis Services 博客](https://blogs.msdn.microsoft.com/analysisservices/)。

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services CTP 2.0
此版本中新添了许多针对表格模型的增强功能，包括：

* 用于保护表格模型元数据的对象级安全性。
* 事务性能改进，开发人员体验响应速度更快。
* 针对实现依赖项分析和报告的 1200 和 1400 模型的动态管理视图改进。
* 对详细信息行表达式的创作体验的改进。
* 层次结构和列重用，在 Power BI 字段列表中更有帮助的位置处显示。
* 日期关系，基于日期字段轻松创建日期维度的关系。
* Analysis Services 的默认安装选项现用于表格模式。
* 新式数据获取 (Power Qery) 数据源。
* 用于 SSDT 的 DAX 编辑器。
* 现有 DirectQuery 数据源支持 M 查询。
* SSMS 改进，例如对结构化数据源的查看、编辑和脚本编写支持。

若要获取有关此 CTP 2.0 版本的更多详细信息，请参阅[Analysis Services 博客](https://blogs.msdn.microsoft.com/analysisservices/)。

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>Windows CTP 1.4 上的 SQL Server Analysis Services
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate)和[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate)预览版本与 SQL Server 2017 预览版本同时发生。 确保使用最新版本以获取新功能。 若要了解详细信息，请参阅[Analysis Services 博客](https://blogs.msdn.microsoft.com/analysisservices/)。



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>Windows CTP 1.3 上的 SQL Server Analysis Services

### <a name="encoding-hints"></a>编码提示

此版本引入了编码提示，这是一种用于优化大型内存中表格模型处理（数据刷新）的高级功能。 若要更好地了解编码，请参阅[性能优化的表格模型中 SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx)更好地了解编码的白皮书。 此处介绍的编码过程适用于 CTP 1.3。

* 值编码为通常仅用于聚合的列提供更好的查询性能。

* 哈希编码首选用于“分组依据”列（通常为维度表值）和外键。 字符串列始终采用哈希编码。

数值列可使用上述任一编码方法。 Analysis Services 开始处理表格时，如果表为空（有或没有分区）或正在执行全表处理操作，则会对每个数值列采用示例值，确定是要应用值编码还是哈希编码。 默认情况下，列中非重复值的示例足够大时会选择值编码，在其他情况下哈希编码通常会提供更好的压缩。 根据数据分布的进一步信息部分处理列后，Analysis Services 可更改编码方法，然后重启编码过程。 当然，这会增加处理时间且效率低下。 性能优化白皮书更详细地讨论了重新编码，并介绍了如何使用 SQL Server Profiler 检测它。

给定数据事件探查的预备知识和/或响应重新编码跟踪事件时，通过 CTP 1.3 中的编码提示，建模器能够指定编码方法的首选项。 由于哈希编码列的聚合速度低于值编码列的聚合速度，因此可将值编码指定为针对此类列的提示。 不能保证该首选项会适用；这是一个提示，而不是设置。 若要指定编码提示，请在列上设置 EncodingHint 属性。 可能的值为“默认”、“值”和“哈希”。 编写时，该属性尚未在 SSDT 中公开，因此必须使用基于 JSON 的元数据、表格模型脚本语言 (TMSL) 或表格对象模型 (TOM) 设置该属性。 Model.bim 文件中基于 JSON 的以下元数据片段为 Sales Amount 列指定值编码。

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

### <a name="extended-events-not-working-in-ctp-13"></a>扩展事件在 CTP 1.3 中无效
SSAS 扩展事件在 CTP 1.3 中无效。 计划在下一版 CTP 中提供修补程序。

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>Windows CTP 1.2 上的 SQL Server Analysis Services

此版本中没有新增功能。 包括 bug 修复和性能改进。

SQL Server Data Tools (SSDT) 的最新预览版与 SQL Server 2017 CTP 1.2 保持一致，它改进了 CTP 1.1 中引入的新式“数据获取”体验，增添了新的查询编辑器菜单和快速访问功能。 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>Windows CTP 1.1 上的 SQL Server Analysis Services 

此版本引入了针对表格模型的增强功能。 

### <a name="1400-compatibility-level-for-tabular-models"></a>针对表格模型的&1400; 兼容级别
  若要充分利用本文所述的特性和功能，新的或现有的表格模型必须设置为 1400 兼容级别。 不能将 1400 兼容级别的模型部署到 SQL Server 2016 SP1 或更早版本，也不能降级为较低的兼容级别。
  
  若要新建或将现有表格模型项目升级到 1400 兼容级别，请下载并安装 **SQL Server Data Tools (SSDT) 17.0 RC2** 的 [预览版本](https://go.microsoft.com/fwlink?LinkId=837939)。 
  
在 SSDT 中，新建表格模型项目时可以选择新的 1400 兼容级别。 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> 12 月发布的 SQL Server Data Tools (SSDT) 中的集成工作区支持 1400 兼容级别。 如果在工作区服务器实例上新建表格模型项目，该实例或任何要部署到的实例必须是 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1。 

要升级现有的表格模型在 SSDT 中，在解决方案资源管理器，请右键单击**Model.bim**，然后在**属性**，将其设置**兼容性级别**属性**SQL Server 自 2017 年 1 (1400)**。 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>新式获取数据体验
SQL Server Data Tools (SSDT) 的最新预览版本与 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 版本一致，它针对 1400 兼容级别的表格模型引入了新式 **获取数据** 体验。 这一新功能基于 Power BI Desktop 和 Microsoft Excel 2016 中类似的功能。

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> 此版本仅支持几种特定的数据源。 未来的更新将支持其他数据源和功能。

若要深入了解新式获取数据体验，请参阅 [Analysis Services Team Blog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/)（Analysis Services 团队博客）。

## <a name="ragged-hierarchies"></a>不规则层次结构
在表格模型中，可以构建父子层次结构模型。 具有不同级别数的层次结构通常称为不规则层次结构。 默认情况下，显示不规则层次结构时，用空白表示低于最低子级的级别。 以下为组织结构图中的不规则层次结构示例：

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

此版本引入了“隐藏成员”  属性。 可以将层次结构的“隐藏成员”  属性设置为“隐藏空成员” 。

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > 模型中的空成员表示为 DAX 空值，而非空字符串。

设置为“隐藏空成员” 并部署模型后，会在报告客户端（如 Excel）中显示易于阅读的层次结构版本。

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>详细信息行
现在可以定义提供度量值的自定义行集。 详细信息行类似于多维模型中的默认钻取操作。 同聚合级别相比，这允许最终用户查看更为详细的信息。 

以下数据透视表显示 Adventure Works 示例表格模型中的年度 Internet 总销售。 可以从度量值中右键单击含有聚合值的单元格，然后单击“显示详细信息”  ，查看详细信息行。

![AS_Show_Details](../analysis-services/media/as-show-details.png)

默认情况下，显示 Internet 销售表中的关联数据。 对用户而言，此限制行为通常没有意义，因为表可能没有必要的列来显示有用信息（如客户名称和订单信息）。 使用详细信息行，可以指定度量值的“详细信息行表达式”  属性。

#### <a name="detail-rows-expression-property-for-measures"></a>度量值的“详细信息行表达式”属性
度量值的“详细信息行表达式”  属性让模型作者能够自定义返回到最终用户的列和行。

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

“详细信息行表达式”中经常使用 [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) DAX 函数。 以下示例定义为示例 Adventure Works 表格模型中 Internet 销售表的行返回的列：

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

定义属性并部署模型后，用户选择“显示详细信息” 时，会返回自定义行集。 它将自动采用所选单元格的筛选上下文。 在此示例中，仅显示 2010 年值的行：

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>表的“默认详细信息行表达式”属性
除了度量值，表还具有一个用于定义详细信息行表达式的属性。 “默认详细信息行表达式”  属性是表中所有度量值的默认值。 没有定义自己的表达式的度量值将继承表中的表达式，并显示为表定义的行集。 这允许重复使用表达式，并且以后添加到表中的新度量值会自动继承该表达式。

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DETAILROWS DAX 函数
此版本包括新的 `DETAILROWS` DAX 函数，该函数返回详细信息行表达式定义的行集。 其工作原理类似于 MDX 中的 `DRILLTHROUGH` 语句，此语句也兼容表格模型中定义的详细信息行表达式。

以下 DAX 查询为度量值或表返回详细信息行表达式定义的行集。 如果未定义任何表达式，会返回 Internet 销售表的数据，因为 Internet 销售表是包含度量值的表。

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>DAX 增强功能
此版本包括 DAX 表达式的 `IN` 运算符。 这与经常用于在 `WHERE` 子句中指定多个值的 [`TSQL IN`](/sql-docs/docs/t-sql/language-elements/in-transact-sql) 运算符类似。

以前，通常使用逻辑 `OR` 运算符指定多值筛选，如以下度量值表达式所示：

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

使用 `IN` 运算符可简化此操作：
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

在这种情况下， `IN` 运算符引用含有 3 行的单列表，每行对应于一种指定的颜色。 请注意，表构造函数语法使用大括号。

`IN` 运算符的功能与 `CONTAINSROW` 函数相同：
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

`IN` 运算符还可和表构造函数有效结合使用。 例如，按产品颜色和类别组合，进行以下度量值筛选：
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

通过新的 `IN` 运算符，以上度量值表达式等效于以下表达式：
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```


## <a name="table-level-security"></a>表级别安全性
此版本引入了表级别安全性。 除了限制对表数据的访问，还可以保护敏感的表名。 这有助于防止恶意用户发现此类表的存在。

必须使用基于 JSON 的元数据、表格模型脚本语言 (TMSL) 或表格对象模型 (TOM) 设置表级别安全性。 

例如，通过将“TablePermission”  类的“MetadataPermission”  属性设置为“无” ，以下代码可帮助保护示例 Adventure Works 表格模型中的产品表。

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```


