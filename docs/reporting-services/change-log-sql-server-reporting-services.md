---
title: SQL Server Reporting Services (SSRS) 2017 及更高版本的更改日志 | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: ''
ms.topic: conceptual
author: casualoak
ms.author: edugonz
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a89c64e6762c2dad2ad9085b27754b3920ffb917
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381245"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 及更高版本的更改日志

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

本文介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的更改内容。 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-140600892-released-august-31-2018"></a>版本 14.0.600.892，发布日期：2018 年 8 月 31 日

已修复以下 bug：

- 当 rc:Toolbar=False 且它具有长文本时，矩形内的文本框导致矩形不沿垂直方向增长 
- 如果 pageHeight 小于 0.5 英寸，则文本大小不会缩放 
- 在与 CRM 一起使用时在 SSRS 目录数据库中发生死锁 
- 在报表中向下滚动时，垂直对齐的列标题不能正确显示 
- 添加到 SCOM Reporting Role 的用户已被阻止访问 SSRS Web 门户 
- 在 PDF 中无法正确导出泰语字符 
- 浏览器角色行为更改 
- rc:Toolbar=false 在 Express Edition 中不起作用 
- 在参数提示区域缺少垂直滚动条 
- 更新了移动报表运行时 

### <a name="version-140600744-released-april-25-2018"></a>版本 14.0.600.744，发布日期：2018 年 4 月 25 日 

已修复以下 bug：

- 创建后，数据驱动订阅页不会显示传递选项
- 将 SSRS 2012 升级到 SSRS 2017 会导致 RSManagement 每几秒钟就引发异常
- 无法更改 IE11 中多值参数的默认值
- 只要执行共享计划，计划就为空

### <a name="version-140600689-released-february-28-2018"></a>版本 14.0.600.689，发布日期：2018 年 2 月 28 日

已修复以下 bug：

- 链接报表中的报表参数可见性在用户编辑它的属性后还原
- URL 参数 rc:Toolbar = false 在 Express edition 中不起作用
- 如果在将 CanGrow 属性设为 false 的文本框中使用表达式，生成的值无法显示
- 为安装程序中的产品密钥添加了“了解更多”链接
- 使用自定义表单身份验证的 Web 门户忽略弹性到期 Cookie
- “导出到 Word”导致行高度不等（如果行内容为空的话）

### <a name="version-140600594-released-january-9-2018"></a>版本 14.0.600.594，发布日期：2018 年 1 月 9 日

安全更新

### <a name="version-140600490-released-november-1-2017"></a>版本 14.0.600.490，发布日期：2017 年 11 月 1 日

已修复以下 bug：

- 已通过 SKU 升级解决问题

### <a name="version-140600451-released-september-30-2017"></a>版本 14.0.600.451，发布日期：2017 年 9 月 30 日 

初始版本

## <a name="next-steps"></a>后续步骤

[Reporting Services (SSRS) 中的新增功能](what-s-new-in-sql-server-reporting-services-ssrs.md)   

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
