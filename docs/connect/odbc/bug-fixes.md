---
title: 修复 bug 列表 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
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
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: 5187e07d18c6a967ce0a8fadbac370273684c9dc
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="list-of-bugs-fixed"></a>修复 bug 的列表

此页包含在每个版本中，从开始修复 bug 的列表[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC 驱动程序 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]的 ODBC 驱动程序 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 修复 1 秒延迟时调用启用了 MARS 的 SQLFreeHandle 和连接属性"Encrypt = yes"
- 修复程序错误 22003 崩溃中 SQLGetData 时传入的缓冲区的大小较小然后正在检索的数据 (Windows)
- 固定截断 ADAL 错误消息
- 修复了极少数 32 位 Windows 上时将转换的浮点数转化为整数
- 修复了问题其中将 double 插入使用始终加密的十进制字段上将不返回数据截断错误
- 在 MacOS 安装程序修复警告
- 修复了不正确状态发送到 SQL Server 会话恢复尝试期间连接复原和连接池都启用时，会导致删除的服务器的会话

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>中的 bug 修复[!INCLUDE[msCoName](../../includes/msconame_md.md)]ODBC 驱动程序 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 修复了 bug 的位置时使用 Kerberos 身份验证，大容量插入可能失败，出现"拒绝访问"错误
- 针对 unixODBC bug 版本低于 2.3.1 中存在已删除的解决方法 （驱动程序翻倍传递给 unixODBC 某些缓冲区的大小）
- 固定连接复原 （重新连接） 时使用 ColumnEncryption 悬挂 = 已启用
- 修复 DSN 创建 bug，其中时使用"Active Directory 交互式身份验证"选项 Azure 身份验证窗口可能会变得不响应 (Windows)
- ODBC 关机期间固定的极少数发生崩溃时异步执行启用 （清除连接句柄时，发生了变化）
- 修复了问题其中 SQL 驱动程序导致执行长时间存储的过程时的高 CPU 占用率
- 固定的无法检索加密 varbinary （max） 列而不进行转换中的数据
- 其中后 null varchar （max） 加密的列使用获取 SQLGetData() 静态游标上修复问题，下列是还音步骤，即使它具有数据
- 修复了问题上提取 varbinary （max） 字段使用始终加密
- 固定 setlocale() 不使用始终加密的问题
- 解决了与 SQLDescribeParam() 返回错误在调用上使用始终加密的 XML 类型的存储过程参数问题
- 不在 SQLTables 中工作的固定转义的下划线
- 修复了 bug 时在 Linux 上作为宽字符为单位返回其中截断希伯来数据 (varchar)
- 修复了问题查询 Shift JIS 编码 char/varchar 从 utf-8 应用程序
- 修复 bug 其中 SQL_DRIVER_NAME 参数调用 SQLGetInfo 返回 Linux 样式 filename 在 MacOS 上
- 修复了问题其中加载 Windows 1252 字符数据，使用输入文件大于 32 k 到使用 BCP 实用工具的 VARCHAR 列的字节将导致故障
