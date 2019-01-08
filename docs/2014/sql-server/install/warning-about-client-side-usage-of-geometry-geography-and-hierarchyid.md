---
title: 关于客户端使用 GEOMETRY、 GEOGRAPHY 和 HIERARCHYID 的警告 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d9ee14c39f7fee577065de934f839f9d6c88e630
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413764"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>关于客户端对 GEOMETRY、GEOGRAPHY 和 HIERARCHYID 的使用的警告
  程序集**Microsoft.SqlServer.Types.dll**，其中包含空间数据类型，具有已从版本 10.0 升级到版本 11.0。 满足某些条件时，引用此程序集的自定义应用程序可能会失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 程序集**Microsoft.SqlServer.Types.dll**，其中包含空间数据类型，具有已从版本 10.0 升级到版本 11.0。 满足以下条件时，引用此程序集的自定义应用程序可能失败：  
  
-   移动时自定义应用程序从一台计算机依据[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]到仅计算机上安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]是安装，该应用程序将失败，因为的被引用的版本 10.0 **SqlTypes**程序集不存在。 你可能会看到以下错误消息：`"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   当引用**SqlTypes**程序集版本 11.0 和也安装了版本 10.0，可能会看到此错误消息： `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   当引用**SqlTypes**从面向.NET 3.5、 4 或 4.5 的自定义应用程序的程序集版本 11.0，该应用程序将失败，因为 SqlClient 按设计加载的程序集的版本 10.0。 当应用程序调用以下方法之一时，将出现此失败：  
  
    -   `GetValue` 类的 `SqlDataReader` 方法  
  
    -   `GetValues` 类的 `SqlDataReader` 方法  
  
    -   `SqlDataReader` 类的方括号索引运算符 []  
  
    -   `ExecuteScalar` 类的 `SqlCommand` 方法  
  
## <a name="corrective-action"></a>纠正措施  
 您可以使用以下方法之一来解决此问题：  
  
-   您可以通过调用 `GetSqlBytes` 方法替代以上所列的 Get 方法来检索 CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统类型，在您的代码中解决此问题，如以下示例中所示：  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   您可以通过在应用程序配置文件中使用程序集重定向来解决此问题，如以下示例中所示：  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   您可以通过为“类型系统版本”属性指定值“SQL Server 2012”以强制 SqlClient 加载程序集的版本 11.0，解决此问题。 此连接字符串属性仅在 .NET 4.5 和更高版本中使用。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
