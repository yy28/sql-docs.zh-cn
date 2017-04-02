---
title: "SQL Server Analysis Services vNext 的新增功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# SQL Server Analysis Services vNext 的新增功能
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>Windows CTP 1.2 上的 SQL Server Analysis Services

此版本中没有新增功能。 包括 bug 修复和性能改进。

与 SQL Server vNext CTP 1.2 一致的 SQL Server Data Tools (SSDT) 的最新预览版改进了 CTP 1.1 中引入的新式 Get Data 体验，包括新的查询编辑器菜单和快速访问功能。 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>Windows CTP 1.1 上的 SQL Server Analysis Services 

此版本引入了针对表格模型的增强功能。 

### <a name="1400-compatibility-level-for-tabular-models"></a>针对表格模型的&1400; 兼容级别
  若要充分利用本文所述的特性和功能，新的或现有的表格模型必须设置为 1400 兼容级别。 不能将 1400 兼容级别的模型部署到 SQL Server 2016 SP1 或更早版本，也不能降级为较低的兼容级别。
  
  若要新建或将现有表格模型项目升级到 1400 兼容级别，请下载并安装 [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939) 的**预览版本**。 
  
在 SSDT 中，新建表格模型项目时可以选择新的 1400 兼容级别。 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE] 12 月发布的 SQL Server Data Tools (SSDT) 中的集成工作区支持 1400 兼容级别。 如果在工作区服务器实例上新建表格模型项目，该实例或任何要部署到的实例必须是 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1。 

若要在 SSDT 中升级现有表格模型，请在“解决方案资源管理器”中右键单击“Model.bim”，然后在“属性”中将“兼容级别”属性设置为“SQL Server vNext (1400)”。 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>新式获取数据体验
SQL Server Data Tools (SSDT) 的最新预览版本与 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 版本一致，它针对 1400 兼容级别的表格模型引入了新式**获取数据**体验。 这一新功能基于 Power BI Desktop 和 Microsoft Excel 2016 中类似的功能。

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE] 此版本仅支持几种特定的数据源。 未来的更新将支持其他数据源和功能。

若要深入了解新式获取数据体验，请参阅 [Analysis Services Team Blog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/)（Analysis Services 团队博客）。

## <a name="ragged-hierarchies"></a>不规则层次结构
在表格模型中，可以构建父子层次结构模型。 具有不同级别数的层次结构通常称为不规则层次结构。 默认情况下，显示不规则层次结构时，用空白表示低于最低子级的级别。 以下为组织结构图中的不规则层次结构示例：

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

此版本引入了“隐藏成员”属性。 可以将层次结构的“隐藏成员”属性设置为“隐藏空成员”。

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE] 模型中的空成员表示为 DAX 空值，而非空字符串。

设置为“隐藏空成员”并部署模型后，会在报告客户端（如 Excel）中显示易于阅读的层次结构版本。

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>详细信息行
现在可以定义提供度量值的自定义行集。 详细信息行类似于多维模型中的默认钻取操作。 同聚合级别相比，这允许最终用户查看更为详细的信息。 

以下数据透视表显示 Adventure Works 示例表格模型中的年度 Internet 总销售。 可以从度量值中右键单击含有聚合值的单元格，然后单击“显示详细信息”，查看详细信息行。

![AS_Show_Details](../analysis-services/media/as-show-details.png)

默认情况下，显示 Internet 销售表中的关联数据。 对用户而言，此限制行为通常没有意义，因为表可能没有必要的列来显示有用信息（如客户名称和订单信息）。 使用详细信息行，可以指定度量值的“详细信息行表达式”属性。

#### <a name="detail-rows-expression-property-for-measures"></a>度量值的“详细信息行表达式”属性
度量值的“详细信息行表达式”属性让模型作者能够自定义返回到最终用户的列和行。

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

定义属性并部署模型后，用户选择“显示详细信息”时，会返回自定义行集。 它将自动采用所选单元格的筛选上下文。 在此示例中，仅显示 2010 年值的行：

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>表的“默认详细信息行表达式”属性
除了度量值，表还具有一个用于定义详细信息行表达式的属性。 “默认详细信息行表达式”属性是表中所有度量值的默认值。 没有定义自己的表达式的度量值将继承表中的表达式，并显示为表定义的行集。 这允许重复使用表达式，并且以后添加到表中的新度量值会自动继承该表达式。

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DETAILROWS DAX 函数
此版本包括新的 `DETAILROWS` DAX 函数，该函数返回详细信息行表达式定义的行集。 其工作原理类似于 MDX 中的 `DRILLTHROUGH` 语句，此语句也兼容表格模型中定义的详细信息行表达式。

以下 DAX 查询为度量值或表返回详细信息行表达式定义的行集。 如果未定义任何表达式，会返回 Internet 销售表的数据，因为 Internet 销售表是包含度量值的表。

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>DAX 增强功能
此版本包括 DAX 表达式的 `IN` 运算符。 这与经常用于在 `WHERE` 子句中指定多个值的 [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) 运算符类似。

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

在这种情况下，`IN` 运算符引用含有 3 行的单列表，每行对应于一种指定的颜色。 请注意，表构造函数语法使用大括号。

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

例如，通过将“TablePermission”类的“MetadataPermission”属性设置为“无”，以下代码可帮助保护示例 Adventure Works 表格模型中的产品表。

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
## <a name="future-updates"></a>未来更新
未来版本将包括其他增强功能。 有关 SQL Server vNext 中新增功能的重要公告发布后，本文将更新。
