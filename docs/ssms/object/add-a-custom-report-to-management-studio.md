---
title: 向 Management Studio 添加自定义报表 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c4459d482fad2639e8aa3ff35dccb38e2aa5cd25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33045234"
---
# <a name="add-a-custom-report-to-management-studio"></a>向 Management Studio 添加自定义报表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
本主题介绍如何创建简单的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 报表并将其保存为 .rdl 文件，然后将该 rdl 文件作为自定义报表添加到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中。 [!INCLUDE[ssRS](../../includes/ssrs_md.md)] 可以创建各式各样的复杂报表。 若要根据本主题创建报表，计算机上必须安装有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 。 不必在 [!INCLUDE[ssRS](../../includes/ssrs_md.md)] 上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ，即可使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]运行自定义报表。  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>创建保存为 .rdl 文件的简单报表  
  
1.  单击“开始”，依次指向“程序”和 “Microsoft SQL Server”，然后单击“SQL Server Data Tools”。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，再单击 **“项目”**。  
  
3.  在 **“项目类型”** 列表中，单击 **“商业智能项目”**。  
  
4.  在“模板”列表中，单击“报表服务器项目向导”。  
  
5.  在“名称”中键入**ConnectionsReport**，再单击“确定”。  
  
6.  在“报表向导”简介页上，单击“下一步”。  
  
7.  在“选择数据源”页上的“名称”框中，键入与 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的连接名称，再单击“编辑”。  
  
8.  在“连接属性”对话框中的“服务器名称”框中，键入 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 实例的名称。  
  
9. 在“选择或输入数据库名称”框中，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 上任意数据库的名称（如 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)]），再单击“确定”。  
  
10. 在“选择数据源”页上，单击“下一步”。  
  
11. 在“设计查询”页上的“查询字符串”框中，键入以下 [!INCLUDE[tsql](../../includes/tsql_md.md)] 语句以列出当前到 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的连接，然后单击“下一步”。 报表向导的“查询字符串”框不接受报表参数。 更为复杂的自定义报表必须以手动方式创建。  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. 在“选择报表类型”页上，选择“表格”，再单击“完成”。  
  
13. 在“完成向导”页上的“报表名称”框中，键入 **ConnectionsReport**，再单击“完成”以创建并保存报表。  
  
14. 关闭 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio_md.md)]。  
  
15. 将 **ConnectionsReport.rdl** 复制到数据库服务器上为自定义报表创建的文件夹中。  
  
### <a name="to-add-a-report-to-management-studio"></a>向 Management Studio 添加报表  
  
-   在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中，右键单击对象资源管理器中的节点，指向“报表”，再单击“自定义报表”。 在“打开文件”对话框中，找到自定义报表文件夹并选择 **ConnectionsReport.rdl** 文件，再单击“打开”。  
  
    第一次从对象资源管理器节点打开新的自定义报表时，该报表将添加到该节点的快捷菜单上“自定义报表”下最近使用的文件列表中。 第一次打开标准报表时，该报表也将出现在“自定义报表”下最近使用的文件列表中。 如果某个自定义报表文件已删除，则下一次选择该项时，系统将提示您从最近使用的文件列表中删除该项。  
  
    1.  若要更改最近使用的文件列表中所显示的文件个数，请在“工具”菜单上单击“选项”，展开“环境”文件夹，再单击“常规”。  
  
    2.  调整“显示最近使用列表中的文件”的数量。  
  
## <a name="see-also"></a>另请参阅  
[Management Studio 中的自定义报表](../../ssms/object/custom-reports-in-management-studio.md)  
[将自定义报表与对象资源管理器节点属性一起使用](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[启用运行自定义报表警告](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](http://msdn.microsoft.com/en-us/b8d18d3d-9db0-43e7-8286-7b46cc3a37ed)  
  
