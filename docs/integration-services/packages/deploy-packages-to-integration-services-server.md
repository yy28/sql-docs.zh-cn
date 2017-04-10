---
title: "将包部署到 Integration Services 服务器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 将包部署到 Integration Services 服务器
  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 引入了增量包部署功能，能够让你将一个或多个包部署到现有或新的项目，而无需部署整个项目。  
  
##  <a name="DeployWizard"></a> 通过使用 Integration Services 部署向导部署包  
  
1.  在命令提示符下，从 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 运行 **isdeploymentwizard.exe**。 在 64 位计算机上，**%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn** 中还有 32 位版本的工具。  
  
2.  在“选择源”  页上，切换到“包部署模型” 。 然后，选择包含源包的文件夹，并配置包。  
  
3.  完成向导。 按照 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)中所述的后续步骤进行操作。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio 部署包  
  
1.  在 SQL Server Management Studio 中，展开对象资源管理器中的“Integration Services 目录” > **SSISDB**节点。  
  
2.  右键单击“项目”文件夹，然后单击“部署项目”。  
  
3.  如果看到“简介”  页，单击“下一步”  以继续。  
  
4.  在“选择源”  页上，切换到“包部署模型” 。 然后，选择包含源包的文件夹，并配置包。  
  
5.  完成向导。 按照 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)中所述的后续步骤进行操作。  
  
##  <a name="SSDT"></a> 使用 SQL Server Data Tools (Visual Studio) 部署包  
  
1.  在 Visual Studio 中，在 Integration Services 项目处于打开状态时，选择一个或多个要部署的包。  
  
2.  右键单击并选择“部署包”。 部署向导将打开，并且所选的包已配置为源包。  
  
3.  完成向导。 按照 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)中所述的后续步骤进行操作。  
  
##  <a name="StoredProcedure"></a> 使用 deploy_packages 存储过程部署包  
 可以使用 **[catalog].[deploy_packages]** 存储过程将一个或多个 SSIS 包部署到 SSIS 目录。 下面的代码示例演示如何通过此存储过程将包部署到 SSIS 服务器。 有关详细信息，请参阅 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)。  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> 使用管理对象模型 API 部署包  
 下面的代码示例演示如何通过管理对象模型 API 将包部署到服务器。  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  