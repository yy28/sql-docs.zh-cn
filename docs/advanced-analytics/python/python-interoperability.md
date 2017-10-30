---
title: "Python 互操作性 |Microsoft 文档"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32762183ff5273998848978238788cc830319b91
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="python-interoperability"></a>Python 互操作性

本主题介绍了当你启用该功能会安装的 Python 组件**机器学习服务 （数据库）**和选择 Python 作为语言。

> [!NOTE]
> 对于 Python 支持是预发行功能，并仍在开发。

## <a name="python-components"></a>Python 组件

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]不会修改 Python 可执行文件。 Python 运行时安装独立于 SQL 工具和外部执行[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]过程。

具有特定关联分发[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]可以与实例关联的文件夹中找到实例。

例如，如果使用默认实例上的 Python 选项安装机器学习服务，查找下：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER`

SQL Server 自 2017 年 1 机器学习 Services 的安装将添加 Python 的 Anaconda 分布。 具体而言，Anaconda 3 安装程序使用时，基于 Anaconda 4.3 分支。 SQL Server 自 2017 年的预期的 Python 级别是 Python 3.5 版。

## <a name="new-in-this-release"></a>此版本中的新增功能

有关支持的 Anaconda 分发的包的列表，请参阅 Continuum 分析站点： [Anaconda 包列表](https://docs.continuum.io/anaconda/pkg-docs)

在 SQL Server 2017 机器学习服务还包括新**revoscalepy** Python 库。

此库提供的功能等效于其中**RevoScaleR**打包成 Microsoft。换而言之，它支持远程计算上下文，以及各种的可缩放的机器学习模型，创建如**rxLinMod**。 有关 RevoScaleR 的详细信息，请参阅[分布式和并行计算与 ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。

因为支持 Python 是预发行功能仍处于开发阶段， **revoscalepy**库目前包括 RevoScaleR 功能的一个子集。 

将来添加可能包括[Microsoft 认知工具包](https://www.microsoft.com/research/product/cognitive-toolkit/)。 以前称为 CNTK，此库支持多种神经网络模型，包括 convolutional 网络 (CNN)、 重复性网络 (RNN) 和长短术语内存网络 (LSTM)。

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

