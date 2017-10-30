---
title: "连接到 dBASE 或其他 DBF 文件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to DBF files
- dBase files
- DBF files
ms.assetid: b0e8c831-9f96-475c-82a4-4f5b02692752
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b1ae38e8b7ba0a9e584a80d1c6cacc76938576a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-dbase-or-other-dbf-file"></a>连接到 dBASE 或其他 DBF 文件
  通过使用 OLE DB 连接管理器并选择 Microsoft OLE DB Provider for Jet 4.0，可以连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中的 dBASE 数据库文件或其他 .DBF 数据库文件。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 SQL Server 导入和导出向导不支持从 dBASE 或其他 DBF 文件中导入，或者导出至 dBASE 或其他 DBF 文件。 您可以使用 Microsoft Access 或 Microsoft Excel 将数据从 DBF 文件导入至 Access 数据库或 Excel 电子表格，然后再使用 SQL Server 导入和导出向导。  
  
### <a name="to-configure-a-connection-manager-to-connect-to-a-dbase-or-other-dbf-file"></a>配置连接管理器以连接到 dBASE 或其他 DBF 文件  
  
1.  向包中添加一个新的 OLE DB 连接管理器。 有关详细信息，请参阅 [Add, Delete, or Share a Connection Manager in a Package](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)。  
  
2.  在“连接管理器”对话框的“连接”页上，请选择“本机 OLE DB\Microsoft Jet 4.0 OLE DB Provider”作为“提供程序”。  
  
3.  使用 DBF 文件时，文件夹表示数据库，单个 DBF 文件表示表。 因此， **“数据库文件名”** 文本框必须包含 DBF 文件所在的文件夹的路径，并且不得包括文件名自身。 您可以键入或粘贴某个文件夹路径，或者使用 **“浏览”** 按钮选择 DBF 文件，然后从文件夹路径的末尾删除文件名。  
  
4.  在“连接管理器”对话框的“全部”页中，根据情况输入 **dBASE III****dBASE IV** 或 **dBASE 5.0** 作为“扩展属性”的值。  
  
5.  单击 **“测试连接”** 验证您输入的值。 应当看到“连接测试成功”消息。 单击“确定”  关闭消息框。  
  
6.  单击 **“确定”** 保存连接管理器的配置。  
  
7.  若要在包的数据流中使用您的连接管理器，请选择 OLE DB 源或目标，并对其进行配置以使用您在上述步骤中创建的连接管理器。  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 连接管理器](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  

