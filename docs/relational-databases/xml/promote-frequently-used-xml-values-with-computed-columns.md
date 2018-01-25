---
title: "使用计算列提升常用的 XML 值 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7374751ae2fd74f93ed0744853eb472689538347
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>使用计算列提升常用的 XML 值
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]如果主要是对少数元素和属性值进行查询，你可能希望将这些数量提升到关系列。 检索整个 XML 实例，但只对一小部分 XML 数据进行查询时，这很有用。 不必对 XML 列创建 XML 索引。 但可以对提升的列进行索引。 必须编写查询才能使用提升的列。 也就是说，查询优化器不会将对 XML 列的查询再定向到提升的列。  
  
 提升的列可以是同一个表中的计算列，也可以是表中用户维护的单独列。 从每个 XML 实例提升单一值时，这就足够了。 但是，对于多值属性，则必须为属性创建单独的表，如下节所述。  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>基于 xml 数据类型的计算列  
 可以使用调用 **xml** 数据类型方法的用户定义函数来创建计算列。 计算列的类型可以是任何 SQL 类型，包括 XML。 下面的示例说明了这一点。  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>示例：基于 xml 数据类型方法的计算列  
 为书的 ISBN 号创建用户定义函数：  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 在表中为 ISBN 添加计算列：  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 可以按通常的方式对计算列创建索引。  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>示例：对基于 xml 数据类型方法的计算列的查询  
 若要获得其 ISBN 为 0-7356-1588-2 的 <`book`>：  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 可以重新编写对 XML 列的查询以使用计算列，如下所示：  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 你可以创建返回 **xml** 数据类型的用户定义函数，并使用用户定义函数来创建计算列。 但是，不能对 XML 计算列创建 XML 索引。  
  
## <a name="creating-property-tables"></a>创建属性表  
 您可能希望将 XML 数据中的某些多值属性提升到一个或多个表中，对那些表创建索引，并再次定向查询以使用这些表。 典型的情况是少数属性占了大部分查询工作负荷。 您可以执行下列操作：  
  
-   创建一个或多个表来保存多值属性。 您会发现可以很方便做到：每个表存储一个属性，以及在属性表中复制基表的主键以便与基表进行后向联接。  
  
-   如果希望维护属性的相对顺序，必须为相对顺序引入一个单独的列。  
  
-   为 XML 列创建触发器以维护属性表。 在触发器中，执行下列操作之一：  
  
    -   使用 **xml** 数据类型方法（如 **nodes()** 和 **value()**）来插入和删除属性表的行。  
  
    -   在公共语言运行时 (CLR) 中创建流式表值函数来插入和删除属性表的行。  
  
    -   编写对属性表进行 SQL 访问的查询和对基表中的 XML 列进行 XML 访问的查询，这些表之间通过主键联接起来。  
  
### <a name="example-create-a-property-table"></a>示例：创建属性表  
 为了进行说明，假定您希望提升作者的名字。 书有一个或多个作者，因此名字为多值属性。 每个名字都存储在属性表的单独行中。 在属性表中复制基表的主键以便进行后向联接。  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>示例：创建用户定义函数以从 XML 实例生成行集  
 以下表值函数 udf_XML2Table 接受主键值和 XML 实例。 它检索 <`book`> 元素的所有作者的名字，然后返回主键-名字对行集。  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>示例：创建触发器以填充属性表  
 插入触发器将行插入属性表：  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 删除触发器根据删除行的主键值删除属性表中的行：  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 更新触发器删除与更新的 XML 实例对应的属性表中的现有行，然后将新行插入属性表：  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>示例：查找其作者名字相同的 XML 实例  
 可以对 XML 列执行此查询。 此外，它也可以在属性表中搜索名字“David”，然后与基表进行后向联接以返回 XML 实例。 例如：  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>示例：使用 CLR 流式表值函数的解决方案  
 此解决方案包括下列步骤：  
  
1.  定义 CLR 类 SqlReaderBase，它实现 ISqlReader，并通过在 XML 实例上应用路径表达式来生成流式表值输出。  
  
2.  创建程序集和 Transact-SQL 用户定义函数来启动该 CLR 类。  
  
3.  通过使用用户定义函数来定义插入、更新和删除触发器，以维护属性表。  
  
 若要如此，首先创建流式 CLR 函数。 **xml** 数据类型在 ADO.NET 中作为托管类 SqlXml 公开，并且支持返回 XmlReader 的 **CreateReader()** 方法。  
  
> [!NOTE]  
>  本部分中的示例代码使用了 XPathDocument 和 XPathNavigator。 这些都强制要求您将所有 XML 文档加载到内存中。 如果您要在您的应用程序中使用类似代码来处理多个大型 XML 文档，此代码并不可伸缩。 而是应尽可能保持较小的内存分配并使用流式接口。 有关性能的详细信息，请参阅 [CLR 集成体系结构](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)。  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 然后，创建一个程序集以及一个对应于 CLR 函数 streaming_xml_tvf 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数 SQL_streaming_xml_tvf（未显示）。 该用户定义函数用于定义表值函数 CLR_udf_XML2Table 以便生成行集：  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 最后，定义触发器，如“创建触发器以填充属性表”示例中所示，但用 CLR_udf_XML2Table 函数替换了 udf_XML2Table。 下面的示例中显示了插入触发器：  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 删除触发器与非 CLR 版本相同。 但是，更新触发器只是用 CLR_udf_XML2Table() 函数替换了函数 udf_XML2Table()。  
  
## <a name="see-also"></a>另请参阅  
 [在计算列中使用 XML](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
  
