---
title: 为 Access 驱动程序以编程方式设置选项 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfb2dca91198c227f03f494fd47f37b7825bcdb8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以编程方式用于访问驱动程序的设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|缓冲区大小|内部缓冲区大小，以千字节为单位，Microsoft Access 用于传输数据与其他磁盘。 默认缓冲区大小为 2048 KB （显示为 2048年）。 可以输入 256 被整除任何整数值。|若要动态设置此选项，在调用中使用 MAXBUFFERSIZE 关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，使用**DSN**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|数据库|而无需选择或创建数据库，可以设置 Microsoft Access 数据源。 如果没有数据库在安装程序时提供的则将提示用户能够连接到数据源时选择某个数据库文件。|若要动态设置此选项，使用**DBQ**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇用日期、 薪金历史记录和当前查看的所有雇员。"|若要动态设置此选项，使用**说明**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|排他|如果**独占**框为选中状态，数据库将以独占方式打开并将一次只能有一个用户可以访问。 以独占模式运行时，为提高性能。|若要动态设置此选项，使用**独占**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|ImplicitCommitSync|确定如何在事务外部所做的更改将写入数据库。 此值最初设置为"是"，这意味着，Microsoft Access 驱动程序将等待完成的内部/隐式事务中的提交。|中包含此选项**设置高级选项**Microsoft Access 驱动程序的对话框。|  
|页超时|指定的时间段，以毫秒为单位，页 （如果未使用） 在被删除之前保留在缓冲区中。 对于 Microsoft Access 驱动程序，默认为 500 毫秒 （0.5 秒为单位）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页 timeout 选项设置为低于该值的过程。|若要动态设置此选项，使用**PAGETIMEOUT**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|只读|将数据库指定为只读的。|若要动态设置此选项，使用**READONLY**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|系统数据库|想要访问与 Microsoft Access 数据库使用的 Microsoft Access 系统数据库的完整路径。<br /><br /> 单击**系统数据库**按钮以选择要使用的系统数据库。 ODBC Microsoft Access 驱动程序会提示用户输入名称和密码。 默认名称是管理员和管理员用户的 Microsoft Access 中的默认密码为空字符串。<br /><br /> 为提高你的 Microsoft Access 数据库的安全性，创建新用户，以替换管理员用户，并删除管理员用户，或更改管理员用户有权访问的对象。|若要动态设置此选项，使用**SYSTEMDB**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|线程|要使用的引擎的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为 3，但可以更改。 用户可能需要增加的线程数，如果没有大量的数据库中的活动。<br /><br /> 中包含此选项**设置高级选项**Microsoft Access 驱动程序的对话框。|若要动态设置此选项，使用**线程**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|UserCommitSync|确定 Microsoft Access 驱动程序是否将以异步方式执行显式的用户定义的事务。 此值最初设置为"是"，这意味着，Microsoft Access 驱动程序将等待中用户定义的事务，若要完成的提交。<br /><br /> 将此选项设置为 False 可以有多用户环境中产生不可预知的后果。|若要动态设置此选项，使用**USERCOMMITSYNC**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|
