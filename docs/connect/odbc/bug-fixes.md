---
title: 修复的 bug 列表 |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 2b939db6ac0f89075b39ba74eadb0e86e63e3980
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041220"
---
# <a name="list-of-bugs-fixed"></a>已修复 bug 的列表

此页列出了每个版本中已修复的 bug 列表，从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 开始

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-1742-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 中的 Bug 修复，适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 - 修复了进程 ID 和应用程序名称无法正确发送到 SQL Server 的问题（对于 sys.databases _exec_sessions 分析）（Linux）
 - 已删除 libuuid 上的冗余依赖项（Linux）
 - 修复了将 UTF8 数据发送到 SQL Server 2019 的 bug
 - 修复了未正确检测以 "@euro" 结尾的区域设置的 bug
 - 修复了在使用 Always Encrypted 时，在将其作为输出参数获取时错误返回的 XML 数据

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-174-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.4 中的 Bug 修复

- 当启用多个活动的结果集（MARS）时修复间歇性挂起
- 启用异步通知时修复连接复原挂起
- 在检索多线程连接尝试的诊断记录时修复崩溃
- 在通过 SQL_USER_NAME 和 SQL_DATA_SOURCE_READ_ONLY 调用 SQLGetInfo （）后，在重新连接后修复 "不支持加密"
- 解决 Azure Active Directory 交互式身份验证期间的 COM 初始化错误
- 修复多字节 UTF8 数据的 SQLGetData （）
- 使用 SQLGetData （）修复 sql_variant 列的检索长度
- 使用 bcp 修复包含7992个以上字节的 sql_variant 列的导入
- 为窄字符数据修复向服务器发送正确编码的问题

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.3 中的 Bug 修复

- 修复了 TCP 发送通知事件句柄内存泄漏
- 修复了 msodbcsql 头文件中枚举 _SQL_FILESTREAM_DESIRED_ACCESS 的重定义问题
- 修复了适用于 Linux 的 msodbcsql 标头文件中缺少的 ACCESS_TOKEN 和身份验证相关定义

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.2 中的 Bug 修复

- 修复了有关 Azure Active Directory 身份验证的错误消息
- 修复了不同区域设置环境变量的固定编码检测
- 修复了断开与连接恢复的连接时的崩溃
- 修复了连接活动的检测
- 修复了已关闭套接字的不正确检测
- 修复了尝试在失败的恢复过程中释放语句句柄时的无限等待
- 修复了版本13和17在 Windows 上安装时的错误卸载行为
- 修复了旧版 Windows 平台上的解密行为（Windows 7、8和 Server 2012）
- 修复了在 Windows 上使用 ADAL 身份验证时的缓存问题
- 修复了在 Windows 上锁定并覆盖跟踪日志的问题

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.1 中的 Bug 修复

- 修复了在启用 MARS 并且连接属性为 "加密 = 是" 的情况调用 SQLFreeHandle 时的1秒延迟
- 修复了传入缓冲区的大小小于所检索的数据的 SQLGetData 中的错误22003崩溃（Windows）
- 修复了截断的 ADAL 错误消息
- 修复了在将浮点数转换为整数时，32位 Windows 上的罕见错误
- 解决了在将双精度插入带 Always Encrypted 的十进制字段的问题时，将返回数据截断错误
- 修复了有关 MacOS 安装程序的警告
- 修复了在启用连接复原和连接池的情况下，在会话恢复尝试期间将错误状态发送到 SQL Server，从而导致服务器删除会话

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 Bug 修复

- 修复了在使用 Kerberos 身份验证时，大容量插入可能会失败并出现 "拒绝访问" 错误的 bug
- 删除了2.3.1 以下版本中存在的 unixODBC bug 的解决方法（驱动程序对传递给 unixODBC 的某些缓冲区大小增加了两倍）
- 修复了使用 ColumnEncryption = enabled 时的连接复原（重新连接）挂起
- 修复了 DSN 创建 bug，使用 "Active Directory Interactive authentication" 选项时，Azure 身份验证窗口可能会变得无响应（Windows）
- 修复了在启用异步执行时 ODBC 关闭（在清除连接句柄时发生）的罕见故障
- 修复了 SQL 驱动程序在执行长时间的存储过程时导致 CPU 使用率高的问题
- 修复了无法在加密的 varbinary （max）列中检索数据的情况
- 修复了在静态游标上使用 SQLGetData （）提取 null varchar （max）加密列后，即使它具有数据，也会空以下列：
- 修复了使用 Always Encrypted 获取 varbinary （max）字段的问题
- 修复了 setlocale （）不能使用 Always Encrypted 的问题
- 修复了在使用 Always Encrypted on 的 XML 类型存储过程参数上调用 SQLDescribeParam （）时返回错误的问题
- 固定的转义下划线在 SQLTables 中不起作用
- 修复了在 Linux 上以宽字符形式返回希伯来语数据（varchar）时截断的 bug
- 修复了从 UTF-8 应用程序查询 Shift-jis-JIS 编码 char/varchar 的问题
- 修复了在调用带有 SQL_DRIVER_NAME 参数的 SQLGetInfo 时，在 MacOS 上返回 Linux 样式文件名的 bug
- 修复了在使用 BCP 实用工具将大于32k 字节的输入文件转换为 VARCHAR 列时，加载 Windows-1252 字符数据的问题会导致失败
