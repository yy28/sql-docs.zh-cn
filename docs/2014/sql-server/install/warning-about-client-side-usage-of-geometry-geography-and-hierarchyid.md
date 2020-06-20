---
title: 有关 GEOMETRY、GEOGRAPHY 和 HIERARCHYID 的客户端使用情况的警告 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 66898aa056800c0a7573b5afa73762785706ff7a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044618"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>关于客户端对 GEOMETRY、GEOGRAPHY 和 HIERARCHYID 的使用的警告
  包含空间数据类型的程序集**Microsoft.SqlServer.Types.dll**已从版本10.0 升级到11.0 版。 满足某些条件时，引用此程序集的自定义应用程序可能会失败。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 包含空间数据类型的程序集**Microsoft.SqlServer.Types.dll**已从版本10.0 升级到11.0 版。 满足以下条件时，引用此程序集的自定义应用程序可能失败：  
  
-   将自定义应用程序从安装了的计算机移 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 到仅安装了的计算机时 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，应用程序将失败，因为**SqlTypes**程序集的引用版本10.0 不存在。 您可能会看到此错误消息：`"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   当引用**SqlTypes**程序集版本11.0 时，还安装了版本10.0，你可能会看到以下错误消息：`"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   如果从以 .NET 3.5、4或4.5 为目标的自定义应用程序引用**SqlTypes**程序集版本11.0，则该应用程序将失败，因为 SqlClient 按设计加载程序集的版本10.0。 当应用程序调用以下方法之一时，将出现此失败：  
  
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
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md
)  
  
  
