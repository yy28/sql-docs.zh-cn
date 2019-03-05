---
title: 修复的缺陷列表 |Microsoft Docs
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
ms.openlocfilehash: 9dba11c0130dc3b969a9fcec46b631abd7d62fe8
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2019
ms.locfileid: "56956048"
---
# <a name="list-of-bugs-fixed"></a>修复的缺陷列表

此页包含在每个版本中，从开始修复的 bug 的列表[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驱动程序 17.3 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 固定的 TCP 发送通知事件句柄内存泄漏
- 枚举 _SQL_FILESTREAM_DESIRED_ACCESS msodbcsql.h 标头文件中的固定重定义问题
- 固定缺少 ACCESS_TOKEN 和身份验证相关的适用于 Linux msodbcsql.h 标头文件中定义

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驱动程序 17.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了 Azure Active Directory 身份验证有关的错误消息
- 修复了编码检测时以不同方式设置区域设置环境变量
- 固定后的故障与恢复正在进行中的连接断开连接
- 修复了检测的连接活动
- 修复了不正确检测的已关闭套接字
- 修复了尝试在失败的恢复期间释放语句句柄时的无限期等待
- Windows 上安装这两个版本 13 和 17 时修复不正确的卸载行为
- 较旧的 Windows 平台 (Windows 7，8 和 Server 2012) 上的固定的解密行为
- 修复时在 Windows 上使用 ADAL 身份验证缓存问题
- 修复了已锁定的问题和 Windows 上的覆盖跟踪日志

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驱动程序 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复 1 秒的延迟时调用启用了 MARS SQLFreeHandle 和连接属性"Encrypt = yes"
- 修复错误 22003 崩溃的 SQLGetData 时传入缓冲区的大小较小，则正在检索的数据 (Windows)
- 修复了截断的 ADAL 错误消息
- 在 32 位 Windows 上修复罕见 bug 时转换浮点数为整数
- 修复了在其中插入十进制字段使用始终加密对双精度返回数据截断错误
- 对 MacOS 的安装程序修复了警告
- 修复了不正确状态发送到 SQL Server 会话恢复尝试期间连接复原和连接池都启用时，从而导致会话由服务器删除

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 修复了 bug 在大容量插入时使用 Kerberos 身份验证，可能会失败，"拒绝访问"错误
- 已删除的版本低于 2.3.1 中存在的 unixODBC bug 的解决方法 （驱动程序增加了一倍的传递给 unixODBC 某些缓冲区的大小）
- 修复了连接复原 （重新连接） 挂起时使用 ColumnEncryption = 启用
- 修复 DSN 创建 bug，其中时使用"Active Directory 交互式身份验证"选项 Azure 身份验证窗口可能会变得无响应 (Windows)
- 在 ODBC 关机固定的极少数崩溃时启用异步执行了 （发生时清除连接句柄）
- 修复了在 SQL 驱动程序，导致执行长时间存储的过程时的高 CPU 占用率
- 修复了无法在无需转换的加密 varbinary （max） 列中检索数据
- 解决了问题，其中后 null varchar （max） 的已加密的列提取对静态游标使用 sqlgetdata （） 过程，下面的列是还空即使它具有的数据
- 修复了与上提取具有始终加密的 varbinary （max） 字段
- 解决了问题 setlocale() 不使用始终加密
- 修复了 SQLDescribeParam() 返回对调用上使用始终加密的 XML 类型的存储过程参数时的错误的问题
- SQLTables 中无法正常工作的固定转义的下划线
- 修复了 bug 在 Linux 上作为宽字符为单位返回时，截断希伯来语数据 (varchar)
- 修复了问题查询 Shift JIS 编码 char/varchar 从 utf-8 应用程序
- 已修复的 bug，调用 SQLGetInfo SQL_DRIVER_NAME 参数返回 Linux 样式文件名在 MacOS 上
- 修复了在其中加载 Windows 1252 字符数据，使用输入文件比使用 BCP 实用工具 VARCHAR 列的字节会导致故障的 32k 大
