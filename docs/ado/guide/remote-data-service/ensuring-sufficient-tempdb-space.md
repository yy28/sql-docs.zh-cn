---
title: "确保足够的 TempDB 空间 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32f05f84953b09f4d727fe6bcba7b4230825faa2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ensuring-sufficient-tempdb-space"></a>确保足够的 TempDB 空间
如果在处理时出现错误[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)需要处理对 Microsoft SQL Server 6.5 的空间的对象，你可能需要增加 TempDB 的大小。 (某些查询需要临时处理空间; 例如，具有 ORDER BY 子句的查询需要排序的**记录集**，这需要一些临时空间。)  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!IMPORTANT]
>  执行操作，因为它不那么容易收缩设备后它展开之前通读此过程。  
  
> [!NOTE]
>  按默认 inMicrosoft 设置 SQL Server 7.0 及更高版本，TempDB 为按需自动增长。 因此，此过程可能仅需要运行版本低于 7.0 的服务器上。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>增加对 SQL Server 6.5 的 TempDB 空间  
  
1.  启动 Microsoft SQL Server 企业管理器，依次打开树的服务器和数据库设备树。  
  
2.  选择一个 （物理） 的设备，若要扩展，如 Master，然后双击该设备，以打开**编辑数据库设备**对话框。  
  
     此对话框显示当前数据库正在使用的空间量。  
  
3.  在**大小**框中，增加为所需的数量 （例如，50 兆字节 (MB) 的硬盘空间） 设备。  
  
4.  单击**立即更改**以提高 （逻辑） TempDB 可以扩展到的空间量。  
  
5.  打开在服务器上，数据库树，然后双击**TempDB**以打开**编辑数据库**对话框。 **数据库**选项卡列出当前分配给 TempDB 空间量 (**数据大小**)。 默认情况下，这是 2 MB。  
  
6.  下**大小**组中，单击**展开**。 图中显示每个物理设备上的可用和已分配空间。 栗色条表示可用空间。  
  
7.  选择**日志中的设备**，例如主，以显示中的可用大小**大小 (MB)**框。  
  
8.  单击**现在展开**分配到 TempDB 数据库该空间。  
  
     **编辑数据库**对话框中显示新为 TempDB 分配大小。  
  
 有关本主题的详细信息，文件中搜索 Microsoft SQL Server 企业管理器帮助"对话框中展开数据库"。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)



