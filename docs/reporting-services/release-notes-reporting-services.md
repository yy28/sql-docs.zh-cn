---
title: 发行说明 (SSRS) 2017年及更高版本 |Microsoft Docs
ms.date: 09/01/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maghan
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: c85d3811fc467d94dc1841b871964e3bb594e2df
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283288"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SQL Server Reporting Services (SSRS) 2017 及更高版本的发行说明

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

本指南介绍了中的更改[!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) 用于 2017年及更高版本。

报表查看器控件的发行说明，请参阅[发行说明，获取报表查看器可以控制对 WebForms 和 WinForms 的 SSRS](application-integration/release-notes-ssrs-application-integration.md)。

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->

## <a name="1406001109-20190212"></a>14.0.600.1109，2019/02/12

| 修复了问题 | 详细信息 |
| :---------- | :------ |
| 缓存报表快照计划在修改订阅后更改为“报表专用计划”。 | &nbsp; |
| rc:Toolbar=false 在 Express Edition 中不起作用。 | &nbsp; |
| 将分页报表导出为 PDF 时，一些泰语字符的呈现不正确。 | &nbsp; |
| 已完成的数据驱动订阅的通知期间出现死锁。 | &nbsp; |
| 使用 rc:Toolbar=False 参数时，嵌入图像在一些情况下不显示。 | &nbsp; |
| 无法为使用级联参数的报表创建数据驱动订阅。 | &nbsp; |
| 无法编辑配置间隔无效的订阅。 | &nbsp; |
| 安全更新。 | &nbsp; |
| 链接的报表 UI 不显示。 | &nbsp; |
| 一些嵌套 Tablix 控件的分页报表的字体不正确。 | &nbsp; |
| 空白错误地添加到某些包含 tablix 数据区域的分页报表。 | &nbsp; |
| 扩展移动报表的简单数据网格时，标题行消失。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906，2018/09/12

已修复以下问题：

| 修复了问题 | 详细信息 |
| :---------- | :------ |
| 自定义身份验证未返回正确的 cookie 信息。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892，2018/08/31

| 修复了问题 | 详细信息 |
| :---------- | :------ |
| 当 rc:Toolbar=False 且它具有长文本时，矩形内的文本框导致矩形不沿垂直方向增长。 | &nbsp; |
| 如果 pageHeight 小于 0.5 英寸，则文本大小不会缩放。 | &nbsp; |
| 它与 CRM 一起使用时，则将发生死锁的 SSRS 目录数据库中。 | &nbsp; |
| 在报表中向下滚动时，垂直对齐的列标题不能正确显示。 | &nbsp; |
| 添加到 SCOM 报表角色的用户已被阻止访问 SSRS Web 门户。 | &nbsp; |
| 到 pdf 文件未能正确导出泰语字符。 | &nbsp; |
| 浏览器角色行为更改。 | &nbsp; |
| rc:Toolbar=false 在 Express Edition 中不起作用。 | &nbsp; |
| 缺少参数提示区域中的垂直滚动条。 | &nbsp; |
| 更新了移动报表运行时。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744，2018/04/25

| 修复了问题 | 详细信息 |
| :---------- | :------ |
| 创建后，数据驱动订阅页不会显示传递选项。 | &nbsp; |
| 将 SSRS 2012 升级到 SSRS 2017 会导致 RSManagement 每几秒钟就引发异常。 | &nbsp; |
| 无法更改 IE11 中多值参数的默认值。 | &nbsp; |
| 只要执行共享的计划，计划就为空。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689，2018/02/28

| 修复了问题 | 详细信息 |
| :---------- | :------ |
| 链接报表中的报表参数可见性在用户编辑它的属性后还原。 | &nbsp; |
| URL 参数 rc:Toolbar = false 在 Express edition 中不起作用。 | &nbsp; |
| 表达式采用 cangrow 文本框属性设置为 false 结果中未显示的值。 | &nbsp; |
| 为安装程序中的产品密钥添加了“了解更多”链接。 | &nbsp; |
| 使用自定义表单身份验证的 Web 门户忽略弹性到期 Cookie。 | &nbsp; |
| “导出到 Word”导致行高度不等（如果行内容为空的话）。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594，2018/01/09

实施一些安全更新。

### <a name="140600490-20171101"></a>14.0.600.490，2017/11/01

已通过 SKU 升级解决问题。

## <a name="140600451-20170930"></a>14.0.600.451，2017/09/30

初始版本。

## <a name="next-steps"></a>后续步骤

[Reporting Services (SSRS) 中的新增功能](what-s-new-in-sql-server-reporting-services-ssrs.md)

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)。
