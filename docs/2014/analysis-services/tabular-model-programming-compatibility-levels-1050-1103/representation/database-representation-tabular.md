---
title: 数据库 Representation(Tabular) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 16a233fb-f83b-4ca1-acb5-6186eca0a62c
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e288ccfb3cee35ef1506fe46d2128dd6ab43480a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197767"
---
# <a name="database-representationtabular"></a>数据库表示形式（表格）
  在表格模式下，数据库为表格模型中所有对象的容器。  
  
## <a name="database-representation"></a>数据库表示形式  
 数据库是构成表格模型的所有对象所在的地方。 开发人员可以查找数据库中包含的连接、表和角色等多种对象。  
  
### <a name="database-in-amo"></a>AMO 中的数据库  
 在使用 AMO 管理表格模型数据库时，AMO 中的 <xref:Microsoft.AnalysisServices.Database> 对象与表格模型中的数据库逻辑对象一对一匹配。  
  
> [!NOTE]  
>  为了获取对 AMO 中数据库对象的访问权限，用户需要有权访问服务器对象并且连接到该服务器对象。  
  
### <a name="database-in-adomdnet"></a>ADOMD.Net 中的数据库  
 在使用 ADOMD 查询表格模型数据库时，通过 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象来获取与特定数据库的连接。  
  
 您可以使用以下代码段直接连接到某个数据库：  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
…  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
…  
  
```  
  
 此外，通过现有连接对象（即尚未关闭），您可以按以下代码段中所示将当前数据库更改为另一数据库：  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>AMO 中的数据库  
 在使用 AMO 管理数据库对象时，请从 <xref:Microsoft.AnalysisServices.Server> 对象开始操作。 然后在数据库集合中搜索您的数据库或通过向集合添加一个数据库来创建新数据库。  
  
 下面的代码段演示用于连接服务器，以及在确定数据库不存在之后创建空数据库的步骤：  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 实际了解如何使用 AMO 创建和操作数据库表示形式，请参阅此表格 AMO 2012 示例; 中的源代码具体查看以下源文件： Database.cs。 示例代码仅作为对此处所述逻辑概念的支持提供，不应用于生产环境中。  
  
  
