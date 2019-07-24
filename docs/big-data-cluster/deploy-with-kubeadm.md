---
title: 配置 Kubernetes 和 kubeadm
titleSuffix: SQL Server big data clusters
description: 了解如何在多个 Ubuntu 16.04 或18.04 计算机 (物理或虚拟) 上配置 Kubernetes, 以进行 SQL Server 2019 大数据群集 (预览版) 部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419446"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>在多台计算机上为 SQL Server 大数据群集部署配置 Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供了有关如何使用**kubeadm**在多台计算机上为 SQL Server 2019 大数据群集 (预览版) 部署配置 Kubernetes 的示例。 在此示例中, 多个 Ubuntu 16.04 或 18.04 LTS 机 (物理或虚拟) 是目标。 如果要部署到不同的 Linux 平台, 则必须更改某些命令以匹配系统。  

> [!TIP] 
> 有关配置 Kubernetes 的示例脚本, 请参阅[在 Ubuntu 16.04 LTS 或 18.04 LTS 上使用 Kubeadm 创建 Kubernetes 群集](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)。

## <a name="prerequisites"></a>先决条件

- 至少3个 Linux 物理计算机或虚拟机
- 每台计算机的建议配置:
   - 8个 Cpu
   - 64 GB 内存
   - 100 GB 存储空间

## <a name="prepare-the-machines"></a>准备计算机

每台计算机上都有几个必需的必备组件。 在 bash 终端中, 在每台计算机上运行以下命令:

1. 将当前计算机添加到`/etc/hosts`文件:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 禁用所有设备上的交换。

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 导入密钥并为 Kubernetes 注册存储库。

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 在计算机上配置 docker 和 Kubernetes 必备组件。

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. 设置 `net.bridge.bridge-nf-call-iptables=1`。 在 Ubuntu 18.04 上, 首先启用`br_netfilter`以下命令。

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>配置 Kubernetes master

在每台计算机上运行上述命令后, 选择一个计算机作为你的 Kubernetes 主机。 然后在该计算机上运行以下命令。

1. 首先, 使用以下命令在当前目录中创建一个 yaml 文件。 

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

1. 初始化此计算机上的 Kubernetes 主节点。 应会看到 Kubernetes 已成功初始化的输出。

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 请注意需要在其他服务器上使用以便加入 Kubernetes 群集的命令。`kubeadm join` 复制以供以后使用。

   ![kubeadm 联接](./media/deploy-with-kubeadm/kubeadm-join.png)

1. 设置主目录的 Kubernetes 配置文件。

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

## <a name="configure-the-kubernetes-agents"></a>配置 Kubernetes 代理

其他计算机将充当群集中的 Kubernetes 代理。 

在其他每台计算机上, 运行`kubeadm join`你在上一部分中复制的命令。

![kubeadm 联接代理](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>查看群集状态

若要验证到群集的连接, 请使用[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令返回群集节点的列表。

```bash
kubectl get nodes
```

## <a name="next-steps"></a>后续步骤

本文中的步骤配置了多个 Ubuntu 计算机上的 Kubernetes 群集。 下一步是部署 SQL Server 2019 大数据群集。 有关说明, 请参阅以下文章:

[在 Kubernetes 上部署 SQL Server](deployment-guidance.md#deploy)
