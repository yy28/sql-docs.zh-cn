---
title: "使用 bcp 连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d2c7f5346d3d834a14161da188733cd72dcede1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-with-bcp"></a>使用 bcp 连接
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[Bcp](http://go.microsoft.com/fwlink/?LinkID=190626)实用工具位于[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上。 此页时记录该对象的 Windows 版本中的差异`bcp`。
  
- 字段终止符是制表符 ("\t")。  
  
- 行终止符是换行符 ("\n")。  
  
- 字符模式是的首选的格式`bcp`格式化文件和不包含扩展的字符的数据文件。  
  
> [!NOTE]  
> 反斜杠\\上的命令行自变量必须是带引号或转义。 例如，若要指定自定义的行终止符作为换行符，必须使用以下机制之一：  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
以下是示例命令调用的`bcp`将表行复制到一个文本文件：  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>可用选项
在当前版本中，以下语法和选项有：  

[*database***.**]*schema***.***table* **in** *data_file* | **out** *data_file*

- -a *packet_size*  
指定服务器发出或接收的每个网络数据包的字节数。  
  
- -b *batch_size*  
指定每批导入数据的行数。  
  
- -c  
使用字符数据类型。  
  
- -d *database_name*  
指定要连接到的数据库。  
  
- -d  
会导致值传递给`bcp`-S 选项被解释为数据源名称 (DSN)。 详细信息，请参阅"在 sqlcmd 和 bcp DSN 支持"中[使用 sqlcmd 连接](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)。  
  
- -e *error_file*指定用来存储任何错误文件的完整路径行`bcp`实用程序无法从文件传输到数据库。  
  
- -e  
将导入数据文件中的一个或多个标识值用于标识列。  
  
- -f *format_file*  
指定格式化文件的完整路径。  
  
- -F *first_row*  
指定要从表中导出或从数据文件导入的第一行的编号。  
  
- -k  
指定在操作过程中空列应该保留 null 值，而不是所插入列的任何默认值。  
  
- -l  
指定登录超时。 – L 选项指定登录名添加到之前的秒数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]当你尝试连接到服务器的超时。 默认登录超时值为 15 秒。 登录超时值必须是介于 0 和 65534 之间的数字。 如果提供的值不是数值或不在此范围内，则 `bcp` 将生成错误消息。 值为 0 指定无限超时。
  
- -L *last_row*  
指定要从表中导出或从数据文件中导入的最后一行的编号。  
  
- -m *max_errors*  
指定的最大前允许发生的语法错误数`bcp`取消操作。  
  
- -n  
使用数据的本机（数据库）数据类型执行大容量复制操作。  
  
- -P *password*  
指定登录 ID 的密码。  
  
- -S  
在 `bcp` 实用工具和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 实例之间的连接中，执行 SET QUOTED_IDENTIFIERS ON 语句。  
  
- -r *row_terminator*  
指定行终止符。  
  
- -r  
指定使用客户端计算机区域设置中定义的区域格式，将货币、日期和时间数据大容量复制到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中。  
  
- -S *server*  
指定的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]要连接到的实例，或者如果-D 使用，DSN。  
  
- -t *field_terminator*  
指定字段终止符。  
  
- -T  
指定`bcp`实用程序连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用可信连接 （集成安全性）。  
  
- -U *login_id*  
指定用于连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的登录 ID。  
  
- -v  
报告 `bcp` 实用工具的版本号和版权。  
  
- -w  
使用 Unicode 字符执行大容量复制操作。  
  
在此版本中，支持 Latin-1 和 UTF-16 字符。  
  
## <a name="unavailable-options"></a>不可用选项
在当前版本中，以下语法和选项不可用：  

- -C  
指定该数据文件中数据的代码页。  
  
- -h *hint*  
指定向表或视图大容量导入数据时所使用的一个或多个提示。  
  
- -i *input_file*  
指定响应文件的名称。  
  
- -n  
对非字符数据使用数据的本机（数据库）数据类型，对字符数据使用 Unicode 字符。  
  
- -o *output_file*  
指定文件名称，该文件用于接收从命令提示符重定向来的输出。  
  
- -V (80 | 90 | 100)  
使用从早期版本的数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
- -x  
结合使用该格式和 -f format_file 选项一起使用，可生成基于 XML 的格式化文件，而不是默认的非 XML 格式化文件。  
  
## <a name="see-also"></a>另请参阅

[使用连接**sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  

