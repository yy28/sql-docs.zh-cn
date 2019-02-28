---
title: SQL Server Reporting Services (SSRS) 2017 及更高版本的更改日志 | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0eec59b0d2618686f866e6b7799922d9c255b238
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56230904"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 及更高版本的更改日志

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

本文介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的更改内容。 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-1406001109-released-february-12-2019"></a>版本 14.0.600.1109，发布时间：2019 年 2 月 12 日

已修复以下问题：

 - 缓存报表快照计划在修改订阅后更改为“报表专用计划”。
 - rc:Toolbar=false 在 Express Edition 中不起作用。
 - 将分页报表导出为 PDF 时，一些泰语字符的呈现不正确。
 - 已完成的数据驱动订阅的通知期间出现死锁
 - 使用 rc:Toolbar=False 参数时，嵌入图像在一些情况下不显示。
 - 无法为使用级联参数的报表创建数据驱动订阅
 - 无法编辑配置间隔无效的订阅。
 - 安全更新
 - 链接的报表 UI 不显示。
 - 一些嵌套 Tablix 控件的分页报表的字体不正确。
 - 向一些包含 Tablix 数据区域的分页报表错误添加空格。
 - 扩展移动报表简单数据网格时，标题行消失。

### <a name="version-140600906-released-september-12-2018"></a>版本 14.0.600.906，发布时间：2018 年 9 月 12 日

已修复以下问题：

- 自定义身份验证未返回正确的 cookie 信息

### <a name="version-140600892-released-august-31-2018"></a>版本 14.0.600.892，发布时间：2018 年 8 月 31 日

已修复以下问题：

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

### <a name="version-140600744-released-april-25-2018"></a>版本 14.0.600.744，发布时间：2018 年 4 月 25 日 

已修复以下问题：

- 创建后，数据驱动订阅页不会显示传递选项
- 将 SSRS 2012 升级到 SSRS 2017 会导致 RSManagement 每几秒钟就引发异常
- 无法更改 IE11 中多值参数的默认值
- 只要执行共享计划，计划就为空

### <a name="version-140600689-released-february-28-2018"></a>版本 14.0.600.689，发布时间：2018 年 2 月 28 日

已修复以下问题：

- 链接报表中的报表参数可见性在用户编辑它的属性后还原
- URL 参数 rc:Toolbar = false 在 Express edition 中不起作用
- 如果在将 CanGrow 属性设为 false 的文本框中使用表达式，生成的值无法显示
- 为安装程序中的产品密钥添加了“了解更多”链接
- 使用自定义表单身份验证的 Web 门户忽略弹性到期 Cookie
- “导出到 Word”导致行高度不等（如果行内容为空的话）

### <a name="version-140600594-released-january-9-2018"></a>版本 14.0.600.594，发布时间：2018 年 1 月 9 日

安全更新

### <a name="version-140600490-released-november-1-2017"></a>版本 14.0.600.490，发布时间：2017 年 11 月 1 日

已修复以下问题：

- 已通过 SKU 升级解决问题

### <a name="version-140600451-released-september-30-2017"></a>版本 14.0.600.451，发布时间：2017 年 9 月 30 日 

初始版本

## <a name="next-steps"></a>后续步骤

[Reporting Services (SSRS) 中的新增功能](what-s-new-in-sql-server-reporting-services-ssrs.md)   

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
