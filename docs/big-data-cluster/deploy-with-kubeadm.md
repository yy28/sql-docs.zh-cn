---
title: 使用 kubeadm 配置 Kubernetes
titleSuffix: SQL Server big data clusters
description: 了解如何配置多个 Ubuntu 16.04 上的 Kubernetes 或用于 SQL Server 2019 大数据群集 （预览版） 部署 18.04 计算机 （物理或虚拟）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 0432f590af92befa845af819269b1111da28251c
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860609"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>配置用于 SQL Server 大数据群集部署的多台计算机上的 Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供有关如何使用的示例**kubeadm**若要配置用于 SQL Server 2019 大数据群集 （预览版） 部署多台计算机上的 Kubernetes。 在此示例中，多个 Ubuntu 16.04 或 18.04 LTS 计算机 （物理或虚拟） 是目标。 如果要部署到不同的 Linux 平台，你必须更改一些命令，以匹配你的系统。  

> [!TIP] 
> 有关配置 Kubernetes 的示例脚本，请参阅[创建 Kubernetes 群集使用 Ubuntu 16.04 LTS 或 18.04 LTS 上 Kubeadm](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)。

## <a name="prerequisites"></a>先决条件

- 3 个 Linux 物理机或虚拟机的最小值
- 每台计算机的推荐的配置：
   - 8 个 Cpu
   - 32 GB 内存
   - 100 GB 的存储

## <a name="prepare-the-machines"></a>准备计算机

每台计算机上有多个所需的先决条件。 在 bash 终端中，每台计算机上运行以下命令：

1. 添加到当前计算机`/etc/hosts`文件：

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 禁用所有设备上交换。

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 导入密钥和对于 Kubernetes 注册存储库。

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 在计算机上配置 docker 和 Kubernetes 的先决条件。

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. 设置 `net.bridge.bridge-nf-call-iptables=1`。 在 Ubuntu 18.04 上的以下命令首先启用`br_netfilter`。

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>将 Kubernetes 主机配置

每台计算机上运行上述命令后, 选择的一台计算机为 Kubernetes 母版。 然后有趣该计算机上的以下命令。

1. 首先，使用以下命令在当前目录中创建一个 rbac.yaml 文件。 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. 初始化此计算机上的 Kubernetes 主机。 应会看到输出 Kubernetes 主机已成功初始化。

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 请注意`kubeadm join`命令需要在其他服务器上用于加入 Kubernetes 群集。 将此内容复制以供将来使用。

   ![kubeadm 联接](./media/deploy-with-kubeadm/kubeadm-join.png)

1. 将 Kubernetes 配置文件设置主目录。

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. 配置群集和 Kubernetes 仪表板。

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>将 Kubernetes 代理配置

在其他计算机将充当 Kubernetes 群集中的代理。 

在每个其他计算机上运行`kubeadm join`在上一部分中复制的命令。

![kubeadm 联接代理](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>查看群集状态

若要验证连接到群集，请使用[kubectl 获取](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令返回群集节点的列表。

```bash
kubectl get nodes
```

## <a name="next-steps"></a>后续步骤

在本文中的步骤配置多台 Ubuntu 计算机上的 Kubernetes 群集。 下一步是部署 SQL Server 2019 大数据群集。 有关说明，请参阅以下文章：

[部署 Kubernetes 上的 SQL Server](deployment-guidance.md#deploy)
