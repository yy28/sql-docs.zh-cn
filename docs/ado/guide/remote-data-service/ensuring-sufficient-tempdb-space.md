---
title: 确保有足够的 TempDB 空间 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e6d558b64095a4071687ed8edd62d54985015c5d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699488"
---
# <a name="ensuring-sufficient-tempdb-space"></a>确保足够的 TempDB 空间
如果在处理时出现错误[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)需要处理在 Microsoft SQL Server 6.5 空间的对象，您可能需要增加 TempDB 的大小。 (某些查询需要的临时处理空间; 例如，包含 ORDER BY 子句的查询需要排序的**记录集**，这需要一些临时空间。)  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!IMPORTANT]
>  执行操作，因为它不是那么简单，它处于展开状态后收缩设备之前请通读此过程。  
  
> [!NOTE]
>  按默认 inMicrosoft 设置 SQL Server 7.0 及更高版本，TempDB 为根据需要自动增加。 因此，此过程只可能有必要运行版本早于 7.0 的服务器上。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>若要增加 SQL Server 6.5 的 TempDB 空间  
  
1.  启动 Microsoft SQL Server 企业管理器中，对于服务器，请打开该树并打开数据库设备树。  
  
2.  选择 （物理） 设备，以扩展，例如 Master，然后双击该设备以打开**编辑数据库设备**对话框。  
  
     此对话框显示当前数据库正在使用的空间量。  
  
3.  在中**大小**框中，增加到所需的量 （例如，50 兆字节 (MB) 的硬盘空间） 设备。  
  
4.  单击**现在更改**以增加的可扩展的 （逻辑） 的 TempDB 空间量。  
  
5.  打开数据库树中的服务器上，并双击**TempDB**以打开**编辑数据库**对话框。 **数据库**选项卡列出了当前分配到 TempDB 的空间量 (**数据大小**)。 默认情况下，这为 2 MB。  
  
6.  下**大小**组中，单击**展开**。 图中显示每个物理设备上可用且已分配空间。 褐紫红色彩色条表示可用空间。  
  
7.  选择**日志中的设备**，例如 Master，以显示中的可用大小**大小 (MB)** 框。  
  
8.  单击**现在展开**分配到 TempDB 数据库的空间。  
  
     **编辑数据库**对话框中显示新分配为 TempDB 的大小。  
  
 有关本主题的详细信息，搜索"展开数据库对话框。"的 Microsoft SQL Server 企业管理器帮助文件  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


