---
title: 选择数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff54dc41b8a39107c191f8976d22005c80d5f65c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216337"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>选择数据源（SQL Server 导入和导出向导）
  使用**选择数据源**页可指定要复制的数据源。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关用于启动向导，选项以及已成功运行该向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 用途[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导，将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **数据源**  
 选择与源的数据存储格式相匹配的数据访问接口。 可用于数据源的访问接口可能不止一个。 例如，对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client、.NET Framework 数据提供程序的 SQL Server 或 Microsoft OLE DB Provider for SQL Server。  
  
 根据计算机上安装的访问接口的不同， **“数据源”** 属性的选项数也会不同。 下表列出了一些常用目标的选项。 有关其他访问接口的信息，请参阅访问接口特定的文档。  
  
## <a name="dynamic-options"></a>动态选项  
 以下部分显示了可用于几种数据源的选项。 此处并未列出“数据源”下拉列表中的所有可用数据源。  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>数据源 = SQL Server Native Client 和 Microsoft OLE DB Provider for SQL Server  
 **服务器名称**  
 键入包含相应数据的服务器的名称，或者从列表中选择服务器。  
  
 **Use Windows Authentication**  
 指定包是否应使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证登录数据库。 为了实现更好的安全性，建议使用 Windows 身份验证。  
  
 **Use SQL Server Authentication**  
 指定包是否应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证来登录到数据库。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 指定数据库连接的用户名称，在使用时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。  
  
 **密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的密码。  
  
 **“数据库”**  
 从指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的数据库列表中选择。  
  
 **“刷新”**  
 通过单击“刷新”，还原可用数据库的列表。  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>数据源 = .NET Framework Data Provider for SQL Server  
 此页显示用于 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据访问接口的选项列表，按字母顺序排列。 下表列出了最重要的选项。  
  
 **数据源**  
 键入包含相应数据的服务器的名称，或者从列表中选择服务器。  
  
 **初始目录**  
 键入源数据库的名称。  
  
 **Integrated Security**  
 指定`True`若要使用 Windows 集成身份验证连接，建议这样做，或`False`若要使用连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果指定 `False`，则必须输入用户 ID 和密码。 默认值是 `False`。  
  
 **用户 ID**  
 指定数据库连接的用户名称，在使用时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。  
  
 **密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的密码。  
  
 选择此访问接口时所列出的其他选项并不是成功连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源数据库所必需。 这些附加选项的说明，请参阅的文档[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]的数据提供程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]软件开发工具包。  
  
### <a name="data-source--microsoft-excel"></a>数据源 = Microsoft Excel  
  
> [!NOTE]  
>  选择**Microsoft Excel**仅当你想要连接到数据源使用 Excel 2003 或更早版本。 若要连接到数据源使用 Excel 2007，选择**Microsoft Office 12.0 Access 数据库引擎 OLE DB 访问接口**，单击**属性**，然后在**所有**选项卡**数据链接属性**对话框框中，输入`Excel 12.0`的值作为**扩展属性**。  
  
 **Excel 文件路径**  
 指定要从其中导入数据的电子表格的路径和文件名。 例如， **C:\MyData.xls， \\\Sales\Database\Northwind.xls**。 或单击 **“浏览”**。  
  
 **“浏览”**  
 通过使用“打开”对话框定位电子表格。  
  
 **Excel 版本**  
 选择存储源数据的 Excel 的版本。  
  
> [!NOTE]  
>  从 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 源导入数据时，向导使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 源组件。 有关使用注意事项和已知问题的信息，请参阅 [Excel Source](../data-flow/excel-source.md)。  
  
### <a name="data-source--microsoft-access"></a>数据源 = Microsoft Access  
  
> [!NOTE]  
>  选择**Microsoft Access**仅当你想要连接到使用 Access 2003 的数据库，或更早版本。 若要连接到使用 Access 2007 数据库，请选择**Microsoft Office 12.0 Access 数据库引擎 OLE DB 访问接口**相反。  
  
 **文件名**  
 指定要从其中导入数据的数据库文件的路径和文件名。 例如，**C:\MyData.mdb、\\\Sales\Database\Northwind.mdb**。 或单击 **“浏览”**。  
  
 **“浏览”**  
 通过使用“打开”对话框定位数据库文件。  
  
 **用户名**  
 当工作组信息文件与数据库关联时，为数据库连接指定一个有效的用户名。  
  
 **密码**  
 当工作组信息文件与数据库关联时，为数据库连接提供相应的用户密码。 但是，如果对于所有用户都使用一个密码保护数据库，则必须在 **“数据链接属性”** 对话框（可通过单击 **“高级”** 访问）中提供此值。  
  
 **高级**  
 您可能想要指定高级的选项，例如数据库密码或非默认工作组信息文件，通过使用**数据链接属性**对话框。 有关 OLE DB 访问接口属性的详细信息，搜索中的数据访问部分[MSDN 库](http://go.microsoft.com/fwlink/?linkid=62553)。  
  
### <a name="data-source--flat-file-source"></a>数据源 = 平面文件源  
 有关平面文件数据源的选项的信息，请参阅以下主题：  
  
 [平面文件连接管理器编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
 [平面文件连接管理器编辑器（“列”页）](../flat-file-connection-manager-editor-columns-page.md)  
  
 [平面文件连接管理器编辑器（“高级”页）](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [平面文件连接管理器编辑器（“预览”页）](../flat-file-connection-manager-editor-preview-page.md)  
  
  
