---
title: "第 8 课： 创建数据筛选器 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea0e116101c9599268b3fc2f3cd556d2149433c8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-8-create-a-data-filter"></a>第 8 课：创建数据筛选器
在父报表上添加钻取操作后，接下来将创建一个数据筛选器，用于为子报表定义的数据表。  
  
可创建基于表的筛选器 **或** 查询筛选器用于钻取报表。 本课对这两种选择均加以说明。  
  
## <a name="table-based-filter"></a>基于表的筛选器  
需要完成以下任务才能实现基于表的筛选器。  
  
-   向子报表中的 tablix 添加一个筛选表达式。  
  
-   创建一个函数，选择未筛选的数据从**PurchaseOrderDetail**表。  
  
-   添加一个事件处理程序，用于将 **PurchaseOrderDetail** DataTable 绑定到子报表。  
  
### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>向子报表中的 tablix 添加一个筛选表达式  
  
1.  打开子报表。  
  
2.  Tablix 中选择一个列标题，右键单击列标题，上面显示的灰色单元，然后选择**Tablix 属性**。  
  
3.  选择**筛选器**页上，然后选择**添加**。  
  
4.  在**表达式**字段，选择**ProductID**从下拉列表。 筛选器即应用于此列。  
  
5.  选择相等 (**=**) 中的运算符**运算符**下拉列表。  
  
6.  选择表达式按钮旁边**值**字段中，选择**参数**中**类别**区域中，，然后双击**productid**中**值**区域。 **设置表达式： 值**字段现在应包含表达式类似于**= 参数 ！ productid。值**。  
  
7.  选择**确定，**和**确定**再次在**Tablix 属性**对话框。  
  
8.  保存 .rdlc 文件。  
  
### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>创建一个函数，用于从 PurchaseOrdeDetail 表选择未筛选的数据  
  
1.  在解决方案资源管理器中，展开 Default.aspx，然后双击 Default.aspx.cs。  
  
2.  创建一个新函数，该函数接受类型为 Integer 的参数 **productid**并返回 **datatable** 对象，然后执行以下操作。  
  
    1.  创建一个数据集 **DataSet2**的实例，该数据集在 [第 4 课：定义用于子报表的数据连接和数据表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)的步骤 2 中创建。  
  
    2.  创建一个到 SqlServer 数据库的连接，以执行在 **第 4 课：定义用于子报表的数据连接和 DataTable**中定义的查询。  
  
    3.  该查询将返回未筛选的数据。  
  
    4.  通过执行该查询，用未筛选的数据填充 DataSet 实例。  
  
    5.  返回 **PurchaseOrderDetail** DataTable。  
  
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
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
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
  
### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>添加一个事件处理程序，用于将 PurchaseOrderDetail DataTable 绑定到子报表  
  
1.  在设计器视图中打开 Default.aspx。  
  
2.  右键单击 ReportViewer 控件，然后选择**属性**。  
  
3.  上**属性**页上，选择**事件**图标。  
  
4.  双击**钻取**事件。  
  
    随后将在代码中添加一个事件处理程序部分，类似于下面这个代码块。  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  将事件处理程序填写完整。 它应包括以下功能。  
  
    1.  从 *DrillthroughEventArgs* 参数提取子报表对象引用。  
  
    2.  调用函数 **GetPurchaseOrderDetail**  
  
    3.  将 **PurchaseOrderDetail** DataTable 与报表的相应数据源绑定。  
  
        填写完整的事件处理程序代码将类似于以下内容。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report.  
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
  
-   创建所选筛选的数据从一个函数**PurchaseOrderDetail**表。  
  
-   添加一个事件处理程序，用于检索参数值并将 **PurchaseOrdeDetail** DataTable 绑定到子报表。  
  
### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>创建一个函数，用于从 PurchaseOrderDetail 表选择经过筛选的数据  
  
1.  在解决方案资源管理器中，展开 Default.aspx，然后双击 Default.aspx.cs。  
  
2.  创建一个新函数，该函数接受类型为 Integer 的参数 **productid**并返回 **datatable** 对象，然后执行以下操作。  
  
    1.  创建一个数据集 **DataSet2**的实例，该数据集在 [第 4 课：定义用于子报表的数据连接和数据表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)的步骤 2 中创建。  
  
    2.  创建一个到 SqlServer 数据库的连接，以执行在 **第 4 课：定义用于子报表的数据连接和 DataTable**中定义的查询。  
  
    3.  该查询将包括参数 **productid**，以确保根据在父报表中选择的 **ProductID** 筛选所返回的数据。  
  
    4.  通过执行该查询，用经过筛选的数据填充 DataSet 实例。  
  
    5.  返回 **PurchaseOrderDetail** DataTable。  
  
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
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlCommand cmd = new SqlCommand("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = @ProductID", sqlconn);  
                  
                        // Sets the productid parameter.  
                        cmd.Parameters.Add((new SqlParameter("@ProductID", SqlDbType.Int)).Value = productid);  
  
                        SqlDataAdapter adap = new SqlDataAdapter(cmd);  
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
  
### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>添加一个事件处理程序，用于检索参数值并将 PurchaseOrdeDetail DataTable 绑定到子报表  
  
1.  在设计器视图中打开 Default.aspx。  
  
2.  右键单击 ReportViewer 控件，然后选择**属性**。  
  
3.  上**属性**窗格中，选择**事件**图标。  
  
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
  
    3.  遍历参数集合并检索从父报表传递的参数 **ProductID**的值。  
  
    4.  调用函数 **GetPurchaseOrderDetail**，并传递参数 **ProductID**的值。  
  
    5.  将 **PurchaseOrderDetail** DataTable 与报表的相应数据源绑定。  
  
        填写完整的事件处理程序代码将类似于以下内容。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report.  
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
您已成功创建了一个数据筛选器，用于为子报表定义的数据表。 接下来，将生成并运行网站应用程序。 请参阅 [第 9 课：生成并运行应用程序](../reporting-services/lesson-9-build-and-run-the-application.md)。  
  
  
  


