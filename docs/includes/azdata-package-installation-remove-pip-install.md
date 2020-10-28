---
author: MikeRayMSFT
ms.prod: sql
ms.topic: include
ms.date: 01/07/2020
ms.author: mikeray
ms.openlocfilehash: 0c15fb58bb076724402ab72f81e58ce46c8b7b1e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257388"
---
### <a name="pythonpip-installation"></a>Python/Pip 安装

可以通过 yum、apt 或 zypper 在 Linux 上安装 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]，也可以通过 Homebrew 安装包管理器在 MacOS 上安装。 在这些包管理器可用之前，需要安装 Python 和 pip。

>[!IMPORTANT]
>在继续之前，需要删除已安装到全局系统 Python 的 `azdata` 的所有安装。 新的安装程序或本机包会将 `azdata` 添加到你的路径中，因此不可能知道哪个是第一个。
如果有已安装到全局系统 Python 的现有 `azdata`，请在继续操作之前将其删除。

若要查看当前安装，请运行以下命令：

```bash
$ pip list --format columns
```

如果 `azdata` 是通过 pip 安装的，则返回包和版本。 例如：

```
 Package             Version
------------------- ----------
azdata-cli          15.0.X
azdata-cli-app      15.0.X
azdata-cli-cluster  15.0.X
azdata-cli-core     15.0.X
azdata-cli-hdfs     15.0.X
azdata-cli-notebook 15.0.X
azdata-cli-profile  15.0.X
azdata-cli-spark    15.0.X
azdata-cli-sql      15.0.X
```

下面的示例删除 `azdata` 的 pip 安装。

```bash
$ pip freeze | grep azdata-* | xargs pip uninstall -y
```

确认已删除通过 pip 安装的 `azdata` 的所有安装后，请继续进行安装。