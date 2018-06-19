---
title: 连接到 Access 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3697fc9f7af68d681dbbc1295e520dd8d7f08f16
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403609"
---
# <a name="connect-to-an-access-database"></a>连接到 Access 数据库
  若要将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包连接到 Microsoft Office Access 数据源，需要使用 OLE DB 连接管理器和数据访问接口。 所使用的数据访问接口取决于创建该数据源的 Access 版本：  
  
-   对于 Access 2003 以及早期版本，该包需要 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 访问接口。  
  
-   对于 Access 2007，该包需要 Microsoft Office 12.0 Access 数据库引擎的 OLE DB 访问接口。  
  
 您可以创建 OLE DB 连接管理器，并从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器的“连接管理器”区域或从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导中选择相应的数据访问接口。  
  
> [!NOTE]  
>  在 64 位计算机上，必须以 32 位模式运行连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 数据源的包。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 访问接口和 Microsoft Office 12.0 Access 数据库引擎的 OLE DB 访问接口仅在 32 位版本下可用。  

## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 和 Access 文件的连接组件
  
可能需要下载 Microsoft Office 文件的连接组件（如果尚未安装）。 在 [Microsoft Access 2016 数据库引擎可再发行（程序包）](https://www.microsoft.com/download/details.aspx?id=54920)中为 Access 和 Excel 文件下载最新版本的连接组件。
  
最新版组件可以打开 Access 早期版本创建的文件。

如果计算机有 32 位版本的 Office，则必须安装 32 位版本的组件，还须确保在 32 位模式下运行程序包。

如果有 Office 365 订阅，请确保下载 Access 数据库引擎 2016 可再发行组件，而不是 Microsoft Access 2016 Runtime。 运行安装程序时，可能会看到一条错误消息，指出该下载项无法与 Office 即点即用组件并行安装。 若要绕过此错误消息，请打开命令提示符窗口并使用 `/quiet` 开关运行下载的 .EXE 文件，从而在安静模式下运行安装。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>连接到 Access 2003 或早期格式的数据源  
  
### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>从“连接管理器”区域创建 Access 连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开该包。  
  
2.  在“连接管理器”区域中，右键单击该区域中的任意位置，然后选择“新建 OLE DB 连接”。  
  
3.  在 **“配置 OLE DB 连接管理器”** 对话框中，单击 **“新建”**。  
  
     有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
4.  在 **“连接管理器”** 对话框中，选择 **“Microsoft Jet 4.0 OLE DB 访问接口”** 作为 **“访问接口”**，然后根据需要配置该连接管理器。  
  
### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>从 SQL Server 导入和导出向导创建 Access 连接  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。  
  
2.  在 **“选择数据源”** 页上，选择 **Microsoft Access**作为 **“数据源”**，然后配置该 Access 连接。  
  
     当选择 **Microsoft Access** 作为 **“数据源”** 时，向导会使用正确的数据访问接口自动创建必要的 OLE DB 连接管理器。 有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>连接到 Access 2007 格式的数据源  
 若要访问 Access 2007 数据源，OLE DB 连接管理器需要 Microsoft Office 12.0 Access 数据库引擎的 OLE DB 访问接口。 此访问接口是随 2007 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office system 自动安装的。 如果在运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的计算机上未安装 2007 Office system，则需要单独安装该访问接口。 若要安装 Microsoft Office 12.0 Access 数据库引擎的 OLE DB 访问接口，请从 [2007 Office System Driver: Data Connectivity Components](http://go.microsoft.com/fwlink/?LinkId=98155)（2007 Office system 驱动程序：数据连接组件）下载并安装这些组件。  
  
### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>从“连接管理器”区域创建 OLE DB 连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开该包。  
  
2.  在“连接管理器”区域中，右键单击该区域中的任意位置，然后选择“新建 OLE DB 连接”。  
  
3.  在 **“配置 OLE DB 连接管理器”** 对话框中，单击 **“新建”**。  
  
     有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
4.  在 **“连接管理器”** 对话框中，选择 **“Microsoft Office 12.0 Access 数据库引擎 OLE DB”** 作为 **“访问接口”**，然后根据需要配置该连接管理器。  
  
    > [!NOTE]  
    >  若要连接到使用 Access 2007 的数据源，则不能选择“Microsoft Jet 4.0 OLE DB 访问接口”作为“数据源”。  
  
### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>从 SQL Server 导入和导出向导创建 OLE DB 连接  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。  
  
2.  在 **“选择数据源”** 页上，选择 **“Microsoft Office 12.0 Access 数据库引擎 OLE DB 访问接口”** 作为 **“数据源”**，然后根据需要配置该连接。  
  
    > [!NOTE]  
    >  若要连接到使用 Access 2007 的数据源，则不能选择“Microsoft Jet 4.0 OLE DB 访问接口”作为“数据源”。  
  
     当选择 **“Microsoft Office 12.0 Access 数据库引擎 OLE DB 访问接口”** 作为 **“数据源”** 时，向导会使用正确的数据访问接口自动创建必要的 OLE DB 连接管理器。 有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
## <a name="see-also"></a>另请参阅  
 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
