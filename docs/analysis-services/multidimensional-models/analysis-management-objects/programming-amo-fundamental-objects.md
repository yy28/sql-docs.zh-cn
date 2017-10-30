---
title: "编程 AMO Fundamental Objects |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- server objects [AMO]
- programming [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
ms.assetid: 3f1ab656-f3bc-432d-8b6d-cdf204e5be10
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0d7e6045e81d10084b0d1951a373f88c675ee083
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-fundamental-objects"></a>AMO 基础对象的编程
  基础对象通常是简单直接的对象。 通常会创建和实例化这些对象，然后在不再需要它们时，用户可以断开与它们的连接。 基础类包括以下对象：<xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.DataSourceView>。 AMO 基础对象中的唯一一个复杂对象是 <xref:Microsoft.AnalysisServices.DataSourceView>，它需要详细信息来生成表示数据源视图的抽象模型。  
  
 将所包含对象用作 OLAP 对象或者数据挖掘对象通常需要 <xref:Microsoft.AnalysisServices.Server> 和 <xref:Microsoft.AnalysisServices.Database> 对象。  
  
 本主题包含以下各节：  
  
-   [服务器对象](#ServerObjects)  
  
-   [AMOException 异常对象](#AMO)  
  
-   [数据库对象](#DatabaseObjects)  
  
-   [数据源对象](#DataSource)  
  
-   [DataSourceView 对象](#DSV)  
  
##  <a name="ServerObjects"></a>服务器对象  
 使用 <xref:Microsoft.AnalysisServices.Server> 对象需要以下步骤：连接服务器，验证 <xref:Microsoft.AnalysisServices.Server> 对象是否已连接到服务器，如果已连接，断开 <xref:Microsoft.AnalysisServices.Server> 与服务器的连接。  
  
### <a name="connecting-to-the-server-object"></a>连接服务器对象  
 连接服务器需要正确的连接字符串。  
  
 下面的代码示例返回<xref:Microsoft.AnalysisServices.Server>对象，如果连接成功，或返回**null**如果发生错误。 连接过程中的错误在 try/catch 构造中处理。 AMO 错误通过 <xref:Microsoft.AnalysisServices.AmoException> 异常类捕获。 在此示例中，错误显示在一个消息框中供用户查看。  
  
```  
static Server ServerConnect( String strStringConnection)  
{  
    string methodCaption = "ServerConnect method";  
    Server svr = new Server();  
    try  
    {  
        svr.Connect(strStringConnection);  
    }  
    #region ErrorHandling  
    catch (AmoException e)  
    {  
        MessageBox.Show( "AMO exception " + e.ToString());  
        svr = null;  
    }  
    catch (Exception e)  
    {  
        MessageBox.Show("General exception " + e.ToString());  
        svr = null;  
    }  
    #endregion  
  
    return svr;  
}  
```  
  
 连接字符串的结构如下：  
  
 "**数据源 =**\<服务器名称 >"。  
  
 有关连接字符串的详细信息，请参阅 <xref:Microsoft.SqlServer.Management.Common.OlapConnectionInfo.ConnectionString%2A>。  
  
### <a name="validating-the-connection"></a>正在验证连接  
 在对 <xref:Microsoft.AnalysisServices.Server> 对象进行编程之前，应验证与服务器仍保持连接。 下面的代码示例演示具体做法。 该示例假定 `svr` 是一个代码中已存在的 <xref:Microsoft.AnalysisServices.Server> 对象。  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    // Do what it is needed if connection is good  
}  
```  
  
### <a name="disconnecting-from-the-server"></a>从服务器断开连接  
 完成之后，可以使用 Disconnect 方法断开与服务器的连接。 下面的代码示例演示具体做法。 该示例假定 `svr` 是一个代码中已存在的 <xref:Microsoft.AnalysisServices.Server> 对象。  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    svr.Disconnect()  
}  
```  
  
###  <a name="AMO"></a>AmoException 异常对象  
 AMO 将在发现各种不同的问题时引发异常。 有关异常的详细说明，请参阅[AMO 其他类和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)。 下面的示例代码演示了捕获 AMO 中的异常的正确方法：  
  
```  
try  
{  
   //... some AMO code in here  
}  
  
catch (  OutOfSynchException e)  
{  
   // error handling code for OutOfSynchException   
}  
  
catch (  OperationException e)  
{  
   // error handling code for OperationException   
}   
  
catch (  ResponseFormatException e)  
  
{  
   // error handling code for ResponseFormatException   
}   
  
catch (  ConnectionException e)  
  
{  
   // error handling code for ConnectionException   
}  
  
catch (  AMOException e)  
  
{  
   //... here is the place where you end if it is an AMO exception, but none of the previous exceptions  
   // if you start with AMOException in the first catch you will never see any one of the previous exceptions  
}  
```  
  
##  <a name="DatabaseObjects"></a>数据库对象  
 使用 <xref:Microsoft.AnalysisServices.Database> 对象非常简单直接。 您可以从 <xref:Microsoft.AnalysisServices.Server> 对象的数据库集合中获取现有数据库。  
  
### <a name="creating-dropping-and-finding-a-database"></a>创建、删除和查找数据库  
 下面的代码示例演示如何使用数据库名称创建数据库。 创建数据库之前，请查询服务器的 <xref:Microsoft.AnalysisServices.DatabaseCollection> 以查看是否存在该数据库。 如果该数据库存在，会将其删除，然后创建该数据库；如果该数据库不存在，将创建它。 如果要删除该数据库，首先要从数据库集合中获取该数据库。  
  
```  
static Database CreateDatabase(Server svr, String DatabaseName)  
{  
    Database db = null;  
    if ( (svr != null) && ( svr.Connected))  
    {  
        // Drop the database if it already exists  
        db = svr.Databases.FindByName(DatabaseName);  
        if (db != null)  
        {  
            db.Drop();  
        }  
  
        // Create the database  
        db = svr.Databases.Add(DatabaseName);  
        db.Update();  
    }  
  
    return db;  
}  
```  
  
 为了确定数据库集合中是否存在某个数据库，可以使用 FindByName 方法。 如果存在该数据库，该方法会返回找到的数据库对象，如果不存在，该方法返回 Null 对象。  
  
 在 <xref:Microsoft.AnalysisServices.Database> 对象添加到数据库集合中后，必须使用服务器的 Update 方法更新服务器。 如果更新服务器失败，则不会在服务器中创建 <xref:Microsoft.AnalysisServices.Database> 对象。  
  
### <a name="processing-a-database"></a>处理数据库  
 处理数据库及其所有子对象很简单，因为 <xref:Microsoft.AnalysisServices.Database> 对象包含一个 Process 方法。  
  
 Process 方法可以包含参数，但不是必需的。 如果未不指定任何参数，则将使用处理所有子对象其**ProcessDefault**选项。 有关处理选项的详细信息，请参阅<xref:Microsoft.AnalysisServices.Database>。  
  
1.  下面的示例代码用数据库的默认值处理数据库。  
  
```  
static Database ProcessDatabase(Database db, ProcessType pt)  
{  
    db.Process( pt);  
    return db;  
}  
```  
  
##  <a name="DataSource"></a>数据源对象  
 <xref:Microsoft.AnalysisServices.DataSource> 对象将 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 与数据所驻留的数据库相链接。 表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 基础模型的架构由 <xref:Microsoft.AnalysisServices.DataSourceView> 对象定义。 <xref:Microsoft.AnalysisServices.DataSource> 对象可视为数据所驻留的数据库的连接字符串。  
  
 下面的示例代码演示如何创建 <xref:Microsoft.AnalysisServices.DataSource> 对象。 该示例验证服务器是否仍然存在，<xref:Microsoft.AnalysisServices.Server> 对象是否已连接以及数据库是否存在。 如果已存在 <xref:Microsoft.AnalysisServices.DataSource> 对象，则将其删除并重新创建。 创建的 <xref:Microsoft.AnalysisServices.DataSource> 对象使用同一名称和内部 ID。 在此示例中，不对连接字符串执行检查来进行验证。  
  
```  
static string CreateDataSource(Database db, string strDataSourceName, string strConnectionString)  
{  
        Server svr = db.Parent;  
        DataSource ds = db.DataSources.FindByName(strDataSourceName);  
        if (ds != null)  
            ds.Drop();  
        // Create the data source  
        ds = db.DataSources.Add(strDataSourceName, strDataSourceName);  
        ds.ConnectionString = strConnectionString;  
  
        // Send the data source definition to the server.  
        ds.Update();  
  
        return ds.Name;  
}  
```  
  
##  <a name="DSV"></a>DataSourceView 对象  
 <xref:Microsoft.AnalysisServices.DataSourceView> 对象负责保存 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的架构模型。 为使 <xref:Microsoft.AnalysisServices.DataSourceView> 对象保存架构，必须先构造架构。 架构基于 System.Data 命名空间中的 DataSet 对象构造。  
  
 下面的示例代码将创建包括在基于 AdventureWorks 的 Analysis Services 示例项目中的部分架构。 该示例创建表、计算列、关系和复合关系的架构定义。 架构是持久化的数据集。  
  
 该示例代码执行下列操作：  
  
1.  创建<xref:Microsoft.AnalysisServices.DataSourceView>对象。  
  
     如果首先验证<xref:Microsoft.AnalysisServices.DataSource>对象存在; 如果**true**，然后删除<xref:Microsoft.AnalysisServices.DataSource>并创建它。 如果 <xref:Microsoft.AnalysisServices.DataSource> 不存在，则创建它。  
  
2.  使用 <xref:Microsoft.AnalysisServices.DataSource> 连接字符串打开与数据库的连接。  
  
3.  创建架构。  
  
     该架构包含以下内容：  
  
    -   表定义，`AddTable()` 方法。  
  
    -   可选计算列集，`AddComputedColumn()` 方法。  
  
    -   可选关系集，`AddRelation`。  
  
    -   可选复合关系集，`AddCompositeRelations`。  
  
4.  更新服务器。  
  
> [!NOTE]  
>  为了阅读方便，下面的示例代码经过了剪裁；完整的代码包含在本主题的末尾。  
  
> [!NOTE]  
>  下面是示例代码中的方法：`AddTable`、`AddComputedColumn`、`AddRelation` 和 `AddCompositeRelation`。  
  
> [!NOTE]  
>  子句`'WHERE 1=0'`是为了避免中返回的行的查询**数据集**对象。  
  
```  
        static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
        {  
            // Create the data source view  
            DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
            if ( dsv != null)  
               dsv.Drop();  
            dsv = db.DataSourceViews.Add(strDataSourceName);  
            dsv.DataSourceID = strDataSourceName;  
            dsv.Schema = new DataSet();  
            dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
            // Open a connection to the data source  
            OleDbConnection connection  
                = new OleDbConnection(dsv.DataSource.ConnectionString);  
            connection.Open();  
  
            #region Create tables  
  
            // Add the DimTime table  
            AddTable(dsv, connection, "DimTime");  
            AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
  
            // Add the DimProductCategory table  
            AddTable(dsv, connection, "DimProductCategory");  
  
            // Add the DimProductSubcategory table  
            AddTable(dsv, connection, "DimProductSubcategory");  
            AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
            // Add the FactInternetSales table  
            AddTable(dsv, connection, "FactInternetSales");  
"DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
  
            // Add the FactInternetSalesReason table  
            AddTable(dsv, connection, "FactInternetSalesReason");  
            AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
            dsv.Update();  
  
            #endregion  
  
            // Send the data source view definition to the server  
            dsv.Update();  
  
            return dsv;  
        }  
  
        static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
        {  
            string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
            OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
            DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
  
            dataTable.ExtendedProperties.Add("TableType", "Table");  
            dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
            dataTable.ExtendedProperties.Add("DbTableName", tableName);  
            dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
        }  
  
        static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
        {  
            DataSet tmpDataSet = new DataSet();  
            tmpDataSet.Locale = CultureInfo.CurrentCulture;  
            OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
                + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
                + tableName + "] WHERE 1=0", connection);  
            DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
            DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
            dataTable.Constraints.Clear();  
            dataTable.Columns.Remove(dataColumn);  
  
            dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
            dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
                expression);  
            dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
            dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
            dataColumn = null;  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
            tmpDataSet = null;  
        }  
  
        static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
        {  
            DataColumn fkColumn  
                = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
            DataColumn pkColumn  
                = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
                + fkColumnName, pkColumn, fkColumn, true);  
        }  
  
        static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
        {  
            DataColumn[] fkColumns = new DataColumn[2];  
            fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
            fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
            DataColumn[] pkColumns = new DataColumn[2];  
            pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
            pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
                + "_" + columnName2, pkColumns, fkColumns, true);  
        }  
  
```  
  
 在示例代码中，`AddTable`和`AddComputedColumn`方法使用`FillSchema`方法**DataAdapter**要添加对象**DataTable**到**数据集**并配置相匹配的数据源中的架构。 扩展属性添加必需的信息以配置 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的架构。  
  
 在该示例代码中，`AddRelation` 和 `AddCompositeRelation` 方法基于模型的现有架构和现有列添加关系列。 列必须是架构中定义的表的一部分，这些方法才能起作用。  
  
 下面是完整的代码示例：  
  
```  
static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
{  
    // Create the data source view  
    DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
    if ( dsv != null)  
       dsv.Drop();  
    dsv = db.DataSourceViews.Add(strDataSourceName);  
    dsv.DataSourceID = strDataSourceName;  
    dsv.Schema = new DataSet();  
    dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
    // Open a connection to the data source  
    OleDbConnection connection  
        = new OleDbConnection(dsv.DataSource.ConnectionString);  
    connection.Open();  
  
    #region Create tables  
  
    // Add the DimTime table  
    AddTable(dsv, connection, "DimTime");  
    AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarYearDesc", "'CY' + ' ' + CalendarYear");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarSemesterDesc", "CASE WHEN CalendarSemester = 1 THEN 'H1'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) ELSE 'H2'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarQuarterDesc", "'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "MonthName", "EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalYearDesc", "'FY' + ' ' + FiscalYear");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalSemesterDesc", "CASE WHEN FiscalSemester = 1 THEN 'H1'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) ELSE 'H2'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalQuarterDesc", "'Q' + CONVERT(CHAR (1), FiscalQuarter) +' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalMonthNumberOfYear", "CASE WHEN MonthNumberOfYear = '1'  THEN CONVERT(int,'7') WHEN MonthNumberOfYear = '2'  THEN CONVERT(int,'8') WHEN MonthNumberOfYear = '3'  THEN CONVERT(int,'9') WHEN MonthNumberOfYear = '4'  THEN CONVERT(int,'10') WHEN MonthNumberOfYear = '5'  THEN CONVERT(int,'11') WHEN MonthNumberOfYear = '6'  THEN CONVERT(int,'12') WHEN MonthNumberOfYear = '7'  THEN CONVERT(int,'1') WHEN MonthNumberOfYear = '8'  THEN CONVERT(int,'2') WHEN MonthNumberOfYear = '9'  THEN CONVERT(int,'3') WHEN MonthNumberOfYear = '10' THEN CONVERT(int,'4') WHEN MonthNumberOfYear = '11' THEN CONVERT(int,'5') WHEN MonthNumberOfYear = '12' THEN CONVERT(int,'6') END");  
    dsv.Update();  
  
    // Add the DimGeography table  
    AddTable(dsv, connection, "DimGeography");  
  
    // Add the DimProductCategory table  
    AddTable(dsv, connection, "DimProductCategory");  
  
    // Add the DimProductSubcategory table  
    AddTable(dsv, connection, "DimProductSubcategory");  
    AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
    // Add the DimProduct table  
    AddTable(dsv, connection, "DimProduct");  
    AddComputedColumn(dsv, connection, "DimProduct", "ProductLineName", "CASE ProductLine WHEN 'M' THEN 'Mountain' WHEN 'R' THEN 'Road' WHEN 'S' THEN 'Accessory' WHEN 'T' THEN 'Touring' ELSE 'Components' END");  
    AddRelation(dsv, "DimProduct", "ProductSubcategoryKey", "DimProductSubcategory", "ProductSubcategoryKey");  
    dsv.Update();  
  
    // Add the DimCustomer table  
    AddTable(dsv, connection, "DimCustomer");  
    AddComputedColumn(dsv, connection, "DimCustomer", "FullName", "CASE WHEN MiddleName IS NULL THEN FirstName + ' ' + LastName ELSE FirstName + ' ' + MiddleName + ' ' + LastName END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "GenderDesc", "CASE WHEN Gender = 'M' THEN 'Male' ELSE 'Female' END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "MaritalStatusDesc", "CASE WHEN MaritalStatus = 'S' THEN 'Single' ELSE 'Married' END");  
    AddRelation(dsv, "DimCustomer", "GeographyKey", "DimGeography", "GeographyKey");  
  
    // Add the DimReseller table  
    AddTable(dsv, connection, "DimReseller");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderFrequencyDesc", "CASE WHEN OrderFrequency = 'A' THEN 'Annual' WHEN OrderFrequency = 'S' THEN 'Bi-Annual' ELSE 'Quarterly' END");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderMonthDesc", "CASE WHEN OrderMonth = '1' THEN 'January' WHEN OrderMonth = '2' THEN 'February' WHEN OrderMonth = '3' THEN 'March' WHEN OrderMonth = '4' THEN 'April' WHEN OrderMonth = '5' THEN 'May' WHEN OrderMonth = '6' THEN 'June' WHEN OrderMonth = '7' THEN 'July' WHEN OrderMonth = '8' THEN 'August' WHEN OrderMonth = '9' THEN 'September' WHEN OrderMonth = '10' THEN 'October' WHEN OrderMonth = '11' THEN 'November' WHEN OrderMonth = '12' THEN 'December' ELSE 'Never Ordered' END");  
  
    // Add the DimCurrency table  
    AddTable(dsv, connection, "DimCurrency");  
    dsv.Update();  
  
    // Add the DimSalesReason table  
    AddTable(dsv, connection, "DimSalesReason");  
  
    // Add the FactInternetSales table  
    AddTable(dsv, connection, "FactInternetSales");  
    AddRelation(dsv, "FactInternetSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactInternetSales", "CustomerKey", "DimCustomer", "CustomerKey");  
    AddRelation(dsv, "FactInternetSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    dsv.Update();  
  
    // Add the FactResellerSales table  
    AddTable(dsv, connection, "FactResellerSales");  
    AddRelation(dsv, "FactResellerSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactResellerSales", "ResellerKey", "DimReseller", "ResellerKey");  
    AddRelation(dsv, "FactResellerSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
  
    // Add the FactInternetSalesReason table  
    AddTable(dsv, connection, "FactInternetSalesReason");  
    AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
    dsv.Update();  
  
    // Add the FactCurrencyRate table  
    AddTable(dsv, connection, "FactCurrencyRate");  
    AddRelation(dsv, "FactCurrencyRate", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    AddRelation(dsv, "FactCurrencyRate", "TimeKey", "DimTime", "TimeKey");  
  
    #endregion  
  
    // Send the data source view definition to the server  
    dsv.Update();  
  
    return dsv;  
}  
  
static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
{  
    string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
    OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
    DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
  
    dataTable.ExtendedProperties.Add("TableType", "Table");  
    dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
    dataTable.ExtendedProperties.Add("DbTableName", tableName);  
    dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
}  
  
static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
{  
    DataSet tmpDataSet = new DataSet();  
    tmpDataSet.Locale = CultureInfo.CurrentCulture;  
    OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
        + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
        + tableName + "] WHERE 1=0", connection);  
    DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
    DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
    dataTable.Constraints.Clear();  
    dataTable.Columns.Remove(dataColumn);  
  
    dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
    dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
        expression);  
    dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
    dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
    dataColumn = null;  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
    tmpDataSet = null;  
}  
  
static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
{  
    DataColumn fkColumn  
        = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
    DataColumn pkColumn  
        = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
        + fkColumnName, pkColumn, fkColumn, true);  
}  
  
static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
{  
    DataColumn[] fkColumns = new DataColumn[2];  
    fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
    fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
    DataColumn[] pkColumns = new DataColumn[2];  
    pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
    pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
        + "_" + columnName2, pkColumns, fkColumns, true);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 基础类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [逻辑体系结构 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

