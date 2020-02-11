---
title: 以编程方式为访问驱动程序设置选项 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 688716e9b7ba89500a4d2e8a579da42972e43d0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063558"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以编程方式为 Access 驱动程序设置选项

|选项|说明|方法|  
|------------|-----------------|------------|  
|缓冲区大小|Microsoft Access 用于将数据传输到磁盘或从磁盘传输数据的内部缓冲区大小（kb）。 默认缓冲区大小为 2048 KB （显示为2048）。 可以输入可被256整除的任何整数值。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用 MAXBUFFERSIZE 关键字。|  
|数据源名称|标识数据源的名称，如工资单或人员。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)时使用**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在安装过程中未提供任何数据库，则在连接到数据源时，系统将提示用户选择数据库文件。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**DBQ**关键字。|  
|说明|数据源中数据的可选说明;例如，"雇用日期、薪金历史记录和所有员工的当前评论"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**DESCRIPTION**关键字。|  
|排他|如果选择了 "**独占**" 框，则数据库将在独占模式下打开，一次只能由一个用户访问。 在独占模式下运行时，性能得到了增强。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**EXCLUSIVE**关键字。|  
|ImplicitCommitSync|确定在事务外进行的更改如何写入数据库。 此值最初设置为 "是"，这意味着 Microsoft Access 驱动程序将等待内部/隐性事务中的提交完成。|此选项包含在 Microsoft Access 驱动程序的 "**设置高级选项**" 对话框中。|  
|页面超时|指定页（如果未使用）在被删除之前保留在缓冲区中的时间段（以毫秒为单位）。 对于 Microsoft Access 驱动程序，默认值为500毫秒（0.5 秒）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时值不能为0。 页面超时值不能小于固有的延迟，即使页面超时选项设置在该值的下面也是如此。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)时使用**READONLY**关键字。|  
|系统数据库|要与要访问的 Microsoft Access 数据库一起使用的 Microsoft Access 系统数据库的完整路径。<br /><br /> 单击 "**系统数据库**" 按钮，选择要使用的系统数据库。 ODBC Microsoft Access 驱动程序提示用户输入名称和密码。 默认名称为 Admin，Microsoft Access 中的 "管理员" 用户的默认密码为空字符串。<br /><br /> 若要提高 Microsoft Access 数据库的安全性，请创建新用户来替换管理员用户并删除管理员用户，或更改管理员用户有权访问的对象。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**SYSTEMDB**关键字。|  
|线程数|引擎要使用的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为3，但可以更改。 如果数据库中有大量活动，则用户可能需要增加线程数。<br /><br /> 此选项包含在 Microsoft Access 驱动程序的 "**设置高级选项**" 对话框中。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**THREADS**关键字。|  
|UserCommitSync|确定 Microsoft Access 驱动程序是否将以异步方式执行显式用户定义事务。 此值最初设置为 "是"，这意味着 Microsoft Access 驱动程序将等待用户定义事务中的提交完成。<br /><br /> 在多用户环境中，将此选项设置为 False 可能会产生不可预知的后果。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的调用中使用**USERCOMMITSYNC**关键字。|
