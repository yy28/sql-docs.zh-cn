---
title: FOR XML 查询与嵌套 FOR XML 查询的比较 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f00e060bf477d6e43f2ddd42e0fd4bbbf6515898
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943348"
---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>FOR XML 查询与嵌套 FOR XML 查询的比较
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主题将单个 FOR XML 查询与嵌套 FOR XML 查询进行了比较。 使用嵌套 FOR XML 查询的好处之一就是可以为查询结果指定一个以属性为中心和以元素为中心的 XML 的组合。 此示例演示了这种好处。  
  
## <a name="example"></a>示例  
 以下 `SELECT` 查询检索 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中的产品类别和子类别信息。 该查询中没有嵌套 FOR XML。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 下面是部分结果：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 如果在查询中指定 `ELEMENTS` 指令，则会收到以元素为中心的结果，如以下结果片段中所示：  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 然后，假设您希望生成一个 XML 层次结构，并且它是以属性为中心和以元素为中心的 XML 组合，则如以下片段中所示：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 在先前的片段中，产品类别信息（如类别 ID 和类别名称）为属性。 但是，子类别信息是以元素为中心的。 若要构造 <`ProductCategory`> 元素，则可以编写 `FOR XML` 查询，如下所示：  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 结果如下：  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 若要在所需的 XML 中构造嵌套 <`ProductSubCategory`> 元素，则可以添加嵌套 `FOR XML` 查询，如下所示：  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 请注意上述查询的以下方面：  
  
-   内部 `FOR XML` 查询检索产品子类别信息。 将 `ELEMENTS` 指令添加到内部 `FOR XML` ，以生成以元素为中心的 XML（它将添加到由外部查询生成的 XML）。 默认情况下，外部查询生成的是以属性为中心的 XML。  
  
-   在内部查询中，指定 `TYPE` 指令以使结果为 **xml** 类型。 如果未指定 `TYPE` ，则结果作为 **nvarchar(max)** 类型返回，XML 数据作为实体返回。  
  
-   外部查询也指定 `TYPE` 指令。 因此，此查询的结果将作为 **xml** 类型返回到客户端。  
  
 下面是部分结果：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 以下查询只是先前查询的扩展。 它显示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中完整的产品层次结构。 其中包括：  
  
-   产品类别  
  
-   每种类别中的产品子类别  
  
-   每种子类别的产品样式  
  
-   每种样式的产品  
  
 您可能会发现以下查询对了解 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库非常有用：  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 下面是部分结果：  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        ...  
    </ProductModel>  
     ...  
```  
  
 如果从生成产品子类别的嵌套 `ELEMENTS` 查询中删除 `FOR XML` 指令，则整个结果均以属性为中心。 然后便可以编写没有嵌套的查询。 添加 `ELEMENTS` 会使 XML 部分以属性为中心、部分以元素为中心。 此结果无法通过单一级别的 FOR XML 查询生成。  
  
## <a name="see-also"></a>另请参阅  
 [使用嵌套 FOR XML 查询](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
