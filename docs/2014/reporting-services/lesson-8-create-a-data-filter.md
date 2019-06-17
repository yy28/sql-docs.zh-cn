---
title: 第 8 课：创建数据筛选器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5204cab43e3c801acf80113ec92c51e00c0f9d13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108390"
---
# <a name="lesson-8-create-a-data-filter"></a>第 8 课：创建数据筛选器
  在父报表上添加钻取操作后，接下来将创建一个数据筛选器，用于为子报表定义的数据表。  
  
 可创建基于表的筛选器 **或** 查询筛选器用于钻取报表。 本课对这两种选择均加以说明。  
  
## <a name="table-based-filter"></a>基于表的筛选器  
 需要完成以下任务才能实现基于表的筛选器。  
  
-   向子报表中的 tablix 添加一个筛选表达式。  
  
-   创建一个函数，用于从 `PurchaseOrderDetail` 表选择未筛选的数据。  
  
-   添加一个事件处理程序，用于将 `PurchaseOrderDetail` DataTable 绑定到子报表。  
  
#### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>向子报表中的 tablix 添加一个筛选表达式  
  
1.  打开子报表。  
  
2.  选择 tablix 中的列标题，右键单击列标题上方显示的灰色单元格，然后单击**Tablix 属性**。  
  
3.  单击**筛选器**页上，然后依次**添加**。  
  
4.  在中**表达式**字段中，单击`ProductID`从下拉列表。 筛选器即应用于此列。  
  
5.  单击等号 ( **=** ) 中的运算符**运算符**下拉列表。  
  
6.  单击表达式按钮旁边**值**字段中，单击**参数**中**类别**区域中，然后再双击`productid`中**值**区域。 **设置表达式：值**字段现在应包含类似于表达式 **= 参数 ！ 产品 id。值**。  
  
7.  单击**确定，** 并**确定**中再次**Tablix 属性**对话框。  
  
8.  保存 .rdlc 文件。  
  
#### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>创建一个函数，用于从 PurchaseOrdeDetail 表选择未筛选的数据  
  
1.  在解决方案资源管理器中，展开 Default.aspx，然后双击 Default.aspx.cs。  
  
2.  创建新的函数接受的参数`productid`，类型为 Integer，并返回`datatable`对象，并执行以下操作。  
  
    1.  创建数据集的实例`DataSet2`，其中的第 2 步中创建[第 4 课：定义用于子报表的数据连接和数据表](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
    2.  创建连接到 SqlServer 数据库以执行中定义的查询**第 4 课：定义数据连接和 DataTable 用于子报表**。  
  
    3.  该查询将返回未筛选的数据。  
  
    4.  通过执行该查询，用未筛选的数据填充 DataSet 实例。  
  
    5.  返回 `PurchaseOrderDetail` DataTable。  
  
         该函数将类似于下面这个函数（仅供参考。 可采用您所需的任意模式提取子报表所需的数据。）  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>添加一个事件处理程序，用于将 PurchaseOrderDetail DataTable 绑定到子报表  
  
1.  打开 Default.aspx。  
  
2.  右键单击 ReportViewer 控件，然后单击**属性。**  
  
3.  上**属性**页上，单击**事件**图标。  
  
4.  双击**钻取**事件。  
  
     随后将在代码中添加一个事件处理程序部分，类似于下面这个代码块。  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  将事件处理程序填写完整。 它应包括以下功能。  
  
    1.  从 *DrillthroughEventArgs* 参数提取子报表对象引用。  
  
    2.  调用函数， `GetPurchaseOrderDetail`  
  
    3.  将 `PurchaseOrderDetail` DataTable 与报表的相应数据源绑定。  
  
         填写完整的事件处理程序代码将类似于以下内容。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  保存该文件。  
  
## <a name="query-filter"></a>查询筛选器  
 需要完成以下任务才能实现查询筛选器。  
  
-   创建一个函数，用于从 `PurchaseOrderDetail` 表选择经过筛选的数据。  
  
-   添加一个事件处理程序，用于检索参数值并将 `PurchaseOrdeDetail` DataTable 绑定到子报表。  
  
#### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>创建一个函数，用于从 PurchaseOrderDetail 表选择经过筛选的数据  
  
1.  在解决方案资源管理器中，展开 Default.aspx，然后双击 Default.aspx.cs。  
  
2.  创建一个新函数，该函数接受类型为 Integer 的参数 `productid` 并返回 `datatable` 对象，然后执行以下操作。  
  
    1.  创建数据集的实例`DataSet2`，其中的第 2 步中创建[第 4 课：定义用于子报表的数据连接和数据表](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
    2.  创建连接到 SqlServer 数据库以执行查询定义**第 4 课：定义数据连接和 DataTable 用于子报表**。  
  
    3.  该查询将包括参数 `productid` 以确保根据在父报表中选择的 `ProductID` 筛选所返回的数据。  
  
    4.  通过执行该查询，用经过筛选的数据填充 DataSet 实例。  
  
    5.  返回 `PurchaseOrderDetail` DataTable。  
  
         该函数将类似于下面这个函数（仅供参考。 可采用您所需的任意模式提取子报表所需的数据。）  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = " + productid, sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>添加一个事件处理程序，用于检索参数值并将 PurchaseOrdeDetail DataTable 绑定到子报表  
  
1.  打开 Default.aspx。  
  
2.  右键单击 ReportViewer 控件，然后依次**属性**。  
  
3.  上**属性**窗格中，单击**事件**图标。  
  
4.  双击**钻取**事件。  
  
     随后将在代码中添加一个事件处理程序部分，类似于以下内容。  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  将事件处理程序填写完整。 它应包括以下功能。  
  
    1.  从 *DrillthroughEventArgs* 参数提取子报表对象引用。  
  
    2.  从所提取的子报表对象获取子报表参数列表。  
  
    3.  遍历参数集合并检索从父报表传递的参数 `ProductID` 的值。  
  
    4.  调用函数 `GetPurchaseOrderDetail` 并传递参数 `ProductID` 的值。  
  
    5.  将绑定`PurchaseOrderDetail`DataTable 与报表的相应数据源。  
  
         填写完整的事件处理程序代码将类似于以下内容。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  保存该文件。  
  
## <a name="next-task"></a>下一个任务  
 您已成功创建了一个数据筛选器，用于为子报表定义的数据表。 接下来，将生成并运行网站应用程序。  
  
  
