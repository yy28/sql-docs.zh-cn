---
title: "与 SQL Server 的 Python 互操作性 |Microsoft 文档"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: ee7187d490c8da80c66fb27156b2726e71782238
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="python-interoperability-with-sql-server"></a>与 SQL Server 的 Python 互操作性

本主题介绍了当你启用该功能会安装的 Python 组件**机器学习服务 （数据库）**和选择 Python 作为语言。

## <a name="python-components"></a>Python 组件

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]不会修改 Python 可执行文件。 Python 运行时安装独立于 SQL 工具和外部执行[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]过程。

具有特定关联分发[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]可以与实例关联的文件夹中找到实例。

例如，如果使用默认实例上的 Python 选项安装机器学习服务，查找下：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

SQL Server 自 2017 年 1 机器学习 Services 的安装将添加 Python 的 Anaconda 分布。 具体而言，Anaconda 3 安装程序使用时，基于 Anaconda 4.3 分支。 SQL Server 自 2017 年的预期的 Python 级别是 Python 3.5 版。

## <a name="new-python-packages-in-this-release"></a>在此版本中的新 Python 包

有关支持的 Anaconda 分发的包的列表，请参阅 Continuum 分析站点： [Anaconda 包列表](https://docs.continuum.io/anaconda/pkg-docs)

在 SQL Server 2017 机器学习服务还包括新**revoscalepy** Python 库。

此库提供的功能等效于其中**RevoScaleR**打包成 Microsoft。换而言之，它支持远程计算上下文，以及各种的可缩放的机器学习模型，创建如**rxLinMod**。 有关 RevoScaleR 的详细信息，请参阅[分布式和并行计算与 ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。

[For Python microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Python 添加到你的安装时，安装将包作为 SQL Server 机器学习的一部分。 此程序包包含许多机器学习算法，经过优化的速度和准确性，以及行用于文本和图像处理的转换。 有关详细信息，请参阅[MicrosoftML 包使用 SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)。

紧密耦合 Microsoftml 和 revoscalepy;在 microsoftml 中使用的数据源被指 revoscalepy 对象。 计算上下文限制到 microsoftml revoscalepy 传输中。 也就是说，对于本地操作，提供了所有功能，但切换到远程计算上下文需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>使用 SQL Server 中的 Python

你导入**revoscalepy**为你的 Python 代码，然后从该模块的调用函数的模块像任何其他 Python 函数。

For Python 的输入的数据必须是表格。 必须在的窗体中返回所有 Python 结果**pandas**数据帧。

可以通过嵌入在存储过程的脚本执行内部 T-SQL 的 Python 代码。

或者，从本地的 Python IDE 运行代码，并有的 SQL Server 计算机上，通过定义远程计算上下文执行的脚本。

你可以使用本地数据、 从 SQL Server 或其他 ODBC 数据源获取数据或使用 XDF 文件格式交换数据与其他源，或与 R 解决方案。

**有关详细信息**

+ 受支持的函数：[什么是 revoscalepy](what-is-revoscalepy.md) 
+ 支持的 Python 数据类型： [Python 库和数据类型](python-libraries-and-data-types.md)
+ 支持的数据源： ODBC 数据库、 SQL Server 和 XDF 文件
+ 支持计算上下文： 本地或 SQL Server

### <a name="licensing"></a>授权

作为使用 Python 的机器学习 Services 的安装的一部分，您必须同意 GNU 公共许可条款。

## <a name="see-also"></a>另请参阅

[Python 库和数据类型](python-libraries-and-data-types.md)
