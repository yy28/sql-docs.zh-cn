---
title: 以编程方式为 Access 驱动程序设置选项 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5227985c56d5e2fd4730c86fe9182c8b16b2cb02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804455"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以编程方式为 Access 驱动程序设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|缓冲区大小|内部缓冲区，以千字节，Microsoft Access 用于传输数据到 \ 来自磁盘的大小。 默认缓冲区大小为 2048 KB （显示为 2048年）。 可以输入任何整除 256 的整数值。|若要动态设置此选项，在调用中使用 MAXBUFFERSIZE 关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，请使用**DSN**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|“数据库”|Microsoft Access 数据源可以设置而无需选择或创建数据库。 如果在安装程序时未不提供任何数据库，将提示用户连接到数据源时选择的数据库文件。|若要动态设置此选项，请使用**DBQ**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇佣日期、 发薪记录和当前查看的所有员工。"|若要动态设置此选项，请使用**描述**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|排他|如果**独占**框处于选中状态，数据库将以独占方式打开，并且一次只能有一个用户可以访问。 以独占模式运行时，性能得到了增强。|若要动态设置此选项，请使用**独占**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|ImplicitCommitSync|确定如何将事务外部所做的更改写入到数据库。 此值最初设置为"是"，意味着 Microsoft Access 驱动程序将等待完成的内部/隐式事务中的提交。|此选项已被纳入**设置高级选项**Microsoft Access 驱动程序对话框。|  
|页超时|以毫秒为单位，页 （如果不使用） 被删除前保留在缓冲区中指定时间的段。 对于 Microsoft Access 驱动程序，默认值为 500 毫秒 （0.5 秒为单位）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页面超时选项设置为低于该值。|若要动态设置此选项，请使用**PAGETIMEOUT**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|只读|指定数据库为只读的。|若要动态设置此选项，请使用**READONLY**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|系统数据库|想要访问与 Microsoft Access 数据库使用的 Microsoft Access 系统数据库的完整路径。<br /><br /> 单击**系统数据库**按钮以选择要使用的系统数据库。 ODBC Microsoft Access 驱动程序会提示用户输入的名称和密码。 默认名称是管理员，管理员用户的 Microsoft Access 中的默认密码为空字符串。<br /><br /> 若要增加你的 Microsoft Access 数据库的安全性，创建新的用户将管理员用户和删除管理员用户，或更改管理员用户有权访问的对象。|若要动态设置此选项，请使用**SYSTEMDB**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|线程|要使用的引擎的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为 3，但可以更改。 用户可能想要增加线程数，如果有大量的数据库中的活动。<br /><br /> 此选项已被纳入**设置高级选项**Microsoft Access 驱动程序对话框。|若要动态设置此选项，请使用**线程**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|UserCommitSync|确定 Microsoft Access 驱动程序是否将以异步方式执行显式的用户定义的事务。 此值最初设置为"是"，意味着 Microsoft Access 驱动程序将等待提交在用户定义事务中才能完成。<br /><br /> 将此选项设置为 False 可以在多用户环境中具有不可预知的后果。|若要动态设置此选项，请使用**USERCOMMITSYNC**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|
