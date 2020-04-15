---
title: 以编程方式设置访问驱动程序的选项 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300787"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以编程方式为 Access 驱动程序设置选项

|选项|描述|方法|  
|------------|-----------------|------------|  
|缓冲区大小|Microsoft Access 用于将数据传输到磁盘和从磁盘传输的内部缓冲区（以千字节为单位）的大小。 默认缓冲区大小为 2048 KB（显示为 2048）。 可以输入任何被 256 整数整数值可分割。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的 MAXBUFFERSIZE 关键字。|  
|数据源名称|标识数据源的名称，如工资单或人员。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在设置时未提供数据库，则在连接到数据源时将提示用户选择数据库文件。|要动态设置此选项，请使用**DBQ**关键字调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、工资历史记录和所有员工的当前审核。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)调用中的 **"描述**"关键字。|  
|排他|如果选择了 **"独占"** 框，则数据库将在独占模式下打开，并且一次只能由一个用户访问。 在独占模式下运行时，性能会增强。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)调用中的**EXCLUSIVE**关键字。|  
|隐式提交同步|确定如何在事务外部所做的更改写入数据库。 此值最初设置为"是"，这意味着 Microsoft Access 驱动程序将等待内部/隐式事务中的提交完成。|此选项包含在 Microsoft 访问驱动程序的 **"设置高级选项**"对话框中。|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以毫秒为单位）。 对于 Microsoft Access 驱动程序，默认值为 500 毫秒（0.5 秒）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时不能为 0。 即使页面超时选项设置为低于该值，页面超时也不能小于固有的延迟。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读数据库。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中的**READONLY**关键字。|  
|系统数据库|要与要访问的 Microsoft Access 数据库一起使用的 Microsoft Access 系统数据库的完整路径。<br /><br /> 单击 **"系统数据库**"按钮以选择要使用的系统数据库。 ODBC 微软访问驱动程序提示用户输入用户名和密码。 默认名称为"管理员"，管理员用户的 Microsoft Access 中的默认密码为空字符串。<br /><br /> 要提高 Microsoft Access 数据库的安全性，请创建新用户以替换管理员用户并删除管理员用户，或更改管理员用户有权访问的对象。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)调用中的**SYSTEMDB**关键字。|  
|线程数|发动机要使用的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为 3，但可以更改。 如果数据库中存在大量活动，用户可能希望增加线程数。<br /><br /> 此选项包含在 Microsoft 访问驱动程序的 **"设置高级选项**"对话框中。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**THREADS**关键字。|  
|用户提交同步|确定 Microsoft Access 驱动程序是否会异步执行显式用户定义的事务。 此值最初设置为"是"，这意味着 Microsoft Access 驱动程序将等待用户定义的事务中的提交完成。<br /><br /> 将此选项设置为 False 可能会在多用户环境中产生不可预知的后果。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**USERCOMMITSYNC**关键字。|
