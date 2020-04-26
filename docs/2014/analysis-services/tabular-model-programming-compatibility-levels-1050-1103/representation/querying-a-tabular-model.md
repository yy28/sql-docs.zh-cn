---
title: 查询表格模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: b01d45d9-4598-4ded-9a9e-e3419cc3df8e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61b6f366843b326a8983c27c3d5ee945604756f0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "62757736"
---
# <a name="querying-a-tabular-model"></a>查询表格模型
  作为开发人员，查询表格模型意味着从表格数据库检索数据；为完成此目标，您具有两个选项：在 DAX 中使用表查询，或者使用 MDX 并且在数据从多维数据集传入时检索数据。 不过，根据您的表格模型的基础模式，您可能会被限制为仅使用 DAX 表查询；DirectQuery 模式要求使用 DAX 表查询。  
  
## <a name="querying-with-adomdnet"></a>使用 ADOMD.Net 进行查询  
 使用 ADOMD.Net 查询表格模型既简单又灵活；您可以将 MDX 语句或表格查询表达式从 DAX 发送到服务器以便获取结果。  
  
 下面的代码演示如何将您的查询语句传递到一个表格模型并接收结果  
  
```csharp  
//Function: tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
//   - arg: qry, the tabular query or MDX expression to be evaluated  
//   - arg: cnx, an active and opened ADOMD connection to the database where 'qry' is to be evaluated  
//  
// This function takes a query or mdx expression -qry-, a connection -cnx-  
// and runs the query it against a Tabular Model using ADOMD.net  
//  
// Important note:  
//    If the MDX query contains more than 2 axes (ON COLUMNS, ON ROWS), each axis will come as a new column  
//    If the (All) value of the members in any axis have not been defined, a blank cell is returned. This might be misleading  
//    if the model also has missing values... which are also represented with blank cells.  
private DataTable tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
{  
    ADOMD.AdomdDataAdapter currentDataAdapter = new ADOMD.AdomdDataAdapter(qry, cnx);  
    DataTable tabularResults = new DataTable();  
    currentDataAdapter.Fill(tabularResults);  
    return tabularResults;  
}  
  
```  
  
### <a name="example"></a>示例  
 如果上面的代码与以下 MDX 表达式一起使用：  
  
```  
SELECT { [Measures].[Internet Total Sales], [Measures].[Reseller Total Sales], [Measures].[Total Sales] } ON COLUMNS  
     , NON EMPTY [Product Category].[Product Category Name].MEMBERS ON ROWS "  
     , NON EMPTY [Date].[Calendar Year].members ON 2 \n"  
FROM [Model]  
  
```  
  
 对于示例模型“Adventure Works DW Tabular Denali CTP3”，您应该收到以下值来作为最终生成的表：  
  
|Calendar Year|Product Category Name|Internet Total Sales|Reseller Total Sales|总销售额|  
|-------------------|---------------------------|--------------------------|--------------------------|-----------------|  
|||$29358677.22|$80450596.98|$109809274.20|  
||Accessories|$700759.96|$571297.93|$1272057.89|  
||Bikes|$28318144.65|$66302381.56|$94620526.21|  
||Clothing|$339772.61|$1777840.84|$2117613.45|  
||组件||$11799076.66|$11799076.66|  
|2001||$3266373.66|$8065435.31|$11331808.96|  
|2001|Accessories||$20235.36|$20235.36|  
|2001|Bikes|$3266373.66|$7395348.63|$10661722.28|  
|2001|Clothing||$34376.34|$34376.34|  
|2001|组件||$615474.98|$615474.98|  
|2002||$6530343.53|$24144429.65|$30674773.18|  
|2002|Accessories||$92735.35|$92735.35|  
|2002|Bikes|$6530343.53|$19956014.67|$26486358.20|  
|2002|Clothing||$485587.15|$485587.15|  
|2002|组件||$3610092.47|$3610092.47|  
|2003||$9791060.30|$32202669.43|$41993729.72|  
|2003|Accessories|$293709.71|$296532.88|$590242.59|  
|2003|Bikes|$9359102.62|$25551775.07|$34910877.69|  
|2003|Clothing|$138247.97|$871864.19|$1010112.16|  
|2003|组件||$5482497.29|$5482497.29|  
|2004||$9770899.74|$16038062.60|$25808962.34|  
|2004|Accessories|$407050.25|$161794.33|$568844.58|  
|2004|Bikes|$9162324.85|$13399243.18|$22561568.03|  
|2004|Clothing|$201524.64|$386013.16|$587537.80|  
|2004|组件||$2091011.92|$2091011.92|  
  
 如果使用以下 DAX 表查询表达式替换该 MDX 表达式：  
  
```  
DEFINE  
   MEASURE 'Product Category'[Internet Sales] = SUM( 'Internet Sales'[Sales Amount])  
   MEASURE 'Product Category'[Reseller Sales] = SUM('Reseller Sales'[Sales Amount]) \n"  
   EVALUATE ADDCOLUMNS('Product Category', \"Internet Sales - All Years\", 'Product Category'[Internet Sales], \"Reseller Sales - All Years\", 'Product Category'[Reseller Sales])  
  
```  
  
 并且使用上述示例代码发送到服务器，则对于示例模型“Adventure Works DW Tabular Denali CTP3”，您应该收到以下值来作为最终生成的表：  
  
|Product Category Id|Product Category Alternate Id|Product Category Name|Internet Sales|Reseller Sales|  
|-------------------------|-----------------------------------|---------------------------|--------------------|--------------------|  
|4|4|Accessories|$700759.96|$571297.93|  
|1|1|Bikes|$28318144.65|$66302381.56|  
|3|3|Clothing|$339772.61|$1777840.84|  
|2|2|组件||$11799076.66|  
  
  
