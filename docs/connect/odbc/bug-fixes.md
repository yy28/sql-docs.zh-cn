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
ms.openlocfilehash: 096c11c018294cbc92b2be13801d6cd953548fff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264010"
---
# <a name="list-of-bugs-fixed"></a>已修复 bug 的列表

此页包含每个版本中已修复的 bug 列表, 从[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.3 中的 Bug 修复[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了 TCP 发送通知事件句柄内存泄漏
- 修复了 msodbcsql 头文件中枚举 _SQL_FILESTREAM_DESIRED_ACCESS 的重定义问题
- 修复了适用于 Linux 的 msodbcsql 标头文件中缺少的 ACCESS_TOKEN 和身份验证相关定义

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.2 中的 Bug 修复[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了有关 Azure Active Directory 身份验证的错误消息
- 修复了不同区域设置环境变量的固定编码检测
- 修复了断开与连接恢复的连接时的崩溃
- 修复了连接活动的检测
- 修复了已关闭套接字的不正确检测
- 修复了尝试在失败的恢复过程中释放语句句柄时的无限等待
- 修复了版本13和17在 Windows 上安装时的错误卸载行为
- 修复了旧版 Windows 平台上的解密行为 (Windows 7、8和 Server 2012)
- 修复了在 Windows 上使用 ADAL 身份验证时的缓存问题
- 修复了在 Windows 上锁定并覆盖跟踪日志的问题

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC 驱动程序17.1 中的 Bug 修复[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了在启用 MARS 并且连接属性为 "加密 = 是" 的情况调用 SQLFreeHandle 时的1秒延迟
- 修复了传入缓冲区的大小小于所检索的数据的 SQLGetData 中的错误22003崩溃 (Windows)
- 修复了截断的 ADAL 错误消息
- 修复了在将浮点数转换为整数时, 32 位 Windows 上的罕见错误
- 解决了在将双精度插入带 Always Encrypted 的十进制字段的问题时, 将返回数据截断错误
- 修复了有关 MacOS 安装程序的警告
- 修复了在启用连接复原和连接池的情况下, 在会话恢复尝试期间将错误状态发送到 SQL Server, 从而导致服务器删除会话

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for 中的 Bug 修复[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了在使用 Kerberos 身份验证时, 大容量插入可能会失败并出现 "拒绝访问" 错误的 bug
- 删除了2.3.1 以下版本中存在的 unixODBC bug 的解决方法 (驱动程序对传递给 unixODBC 的某些缓冲区大小增加了两倍)
- 修复了使用 ColumnEncryption = enabled 时的连接复原 (重新连接) 挂起
- 修复了 DSN 创建 bug, 使用 "Active Directory Interactive authentication" 选项时, Azure 身份验证窗口可能会变得无响应 (Windows)
- 修复了在启用异步执行时 ODBC 关闭 (在清除连接句柄时发生) 的罕见故障
- 修复了 SQL 驱动程序在执行长时间的存储过程时导致 CPU 使用率高的问题
- 修复了无法在加密的 varbinary (max) 列中检索数据的情况
- 修复了在静态游标上使用 SQLGetData () 提取 null varchar (max) 加密列后, 即使它具有数据, 也会空以下列:
- 修复了使用 Always Encrypted 获取 varbinary (max) 字段的问题
- 修复了 setlocale () 不能使用 Always Encrypted 的问题
- 修复了在使用 Always Encrypted on 的 XML 类型存储过程参数上调用 SQLDescribeParam () 时返回错误的问题
- 固定的转义下划线在 SQLTables 中不起作用
- 修复了在 Linux 上以宽字符形式返回希伯来语数据 (varchar) 时截断的 bug
- 修复了从 UTF-8 应用程序查询 Shift-jis-JIS 编码 char/varchar 的问题
- 修复了在调用带有 SQL_DRIVER_NAME 参数的 SQLGetInfo 时, 在 MacOS 上返回 Linux 样式文件名的 bug
- 修复了在使用 BCP 实用工具将大于32k 字节的输入文件转换为 VARCHAR 列时, 加载 Windows-1252 字符数据的问题会导致失败
