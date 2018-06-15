---
title: SQL Server Reporting Services 更改日志（2017 及更高版本）| Microsoft Docs
ms.custom: ''
ms.date: 04/25/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: casualoak
ms.author: edugonz
manager: kfile
ms.openlocfilehash: ee37f4445a02925c0017f67d3f25056b047a1f05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014194"
---
# <a name="change-log-for-sql-server-reporting-services"></a>SQL Server Reporting Services 的更改日志

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

本文介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的更改内容。 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

- 版本 14.0.600.744，发布日期：2018 年 4 月 25 日 
    - Bug 修复：
        - 创建后，数据驱动订阅页不会显示传递选项
        - 将 SSRS 2012 升级到 SSRS 2017 会导致 RSManagement 每几秒钟就引发异常
        - 无法更改 IE11 中多值参数的默认值
        - 只要执行共享计划，计划就为空

- 版本 14.0.600.689（发布日期：2018 年 2 月 28 日） 
    - Bug 修复：
        - 链接报表中的报表参数可见性在用户编辑它的属性后还原
        - URL 参数 rc:Toolbar = false 在 Express edition 中不起作用
        - 如果在将 CanGrow 属性设为 false 的文本框中使用表达式，生成的值无法显示
        - 为安装程序中的产品密钥添加了“了解更多”链接
        - 使用自定义表单身份验证的 Web 门户忽略弹性到期 Cookie
        - “导出到 Word”导致行高度不等（如果行内容为空的话）

- 版本 14.0.600.594，发布日期：2018 年 1 月 9 日
    - 安全更新

- 版本 14.0.600.490，发布日期：2017 年 11 月 1 日 
    - Bug 修复：
        - 已通过 SKU 升级解决问题

- 版本 14.0.600.451，发布日期：2017 年 9 月 30 日 
    - 初始版本

## <a name="next-steps"></a>后续步骤

[Reporting Services (SSRS) 中的新增功能](what-s-new-in-sql-server-reporting-services-ssrs.md)   

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
