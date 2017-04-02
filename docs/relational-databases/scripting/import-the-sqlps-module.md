---
title: "导入 SQLPS 模块 | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: 12
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 导入 SQLPS 模块
  从 PowerShell 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的建议方法是将 **sqlps** 模块导入到 Windows PowerShell 环境中。 该模块将加载并注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理单元和可管理性程序集。  从 Windows PowerShell 3.0 开始，在命令中使用模块的任意 cmdlet 或函数时会自动导入该模块。 此功能对目录中的任何模块均有效，该目录包含在 PSModulePath 环境变量的值中。  有关其他信息，请参阅[导入 PowerShell 模块](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx)
  
1.  **开始之前：**  [安全性](#Security)  
  
2.  **若要加载模块，请执行以下操作：**  [加载 sqlps 模块](#LoadSqlps)  
  
## 开始之前  
 在将 **sqlps** 模块导入到 Windows PowerShell 后，您可以：  
  
-   以交互方式运行 Windows PowerShell 命令。  
  
-   运行 Windows PowerShell 脚本文件。  
  
-   运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序路径可以浏览 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的层次结构。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可管理性对象模型（例如 Microsoft.SqlServer.Management.Smo）管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象。  
  
> [!NOTE]  
>  在两个 SQL Server cmdlet（**Encode-Sqlname** 和 **Decode-Sqlname**）的名称中使用的动词与 Windows PowerShell 批准的动词不匹配。 这对其操作没有影响，但在将 **sqlps** 模块导入到某一会话时 Windows PowerShell 将引发警告。  
  
###  <a name="Security"></a> 安全性  
 默认情况下，Windows PowerShell 会在脚本执行策略设置为 **Restricted**（即，禁止运行任何 Windows PowerShell 脚本）的情况下运行。 若要加载 **sqlps** 模块，你可以使用 **Set-ExecutionPolicy** cmdlet 来运行已签名脚本或任意脚本。 请仅运行来自受信任源的脚本，并通过使用适当的 NTFS 权限来保证所有输入和输出文件的安全。 有关启用 Windows PowerShell 脚本的详细信息，请参阅 [Running Windows PowerShell Scripts](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)（运行 Windows PowerShell 脚本）。  
  
##  <a name="LoadSqlps"></a> 加载 sqlps 模块  
 **加载 Windows PowerShell 中的 sqlps 模块**  
  
1.  使用 **Set-ExecutionPolicy** cmdlet 设置相应的脚本执行策略。  
  
2.  使用 **Import-Module** cmdlet 导入 sqlps 模块。 如果你想要不显示与 **Encode-Sqlname** 和 **Decode-Sqlname** 有关的警告，请指定 **DisableNameChecking** 参数。  
  
### 示例  
 此示例加载 **sqlps** 模块并且禁用了名称检查。  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  如果 **sqlps** 模块不在你的路径下，请更改为模块的位置或在脚本中使用完整路径（在路径中对文件夹使用双引号，其中包含空格）。 **sqlps** 模块位于 SQL Server 实例的 Tools\Powershell 文件夹中。  
  
 ![用于“返回首页”链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.png "用于“返回首页”链接的箭头图标") [[返回页首]](#Intro)  
  
## 另请参阅  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [使用数据库引擎 cmdlet](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [安装 PowerShell 模块](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  