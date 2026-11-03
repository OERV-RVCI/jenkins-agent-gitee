# README.md


https://openeulerjenkins.osinfra.cn/job/EBS-OS-build/下riscv64架构镜像制作的运行镜像   
openjdk11-Dockerfile 已弃用   
openjdk17-Dockerfile 正在使用   

## 镜像制作流水线

通过 GitHub Actions(`.github/workflows/docker-image.yml`)自动构建并推送镜像。
向对应分支推送对 `openjdk17-Dockerfile` 的变更时自动触发,也可手动触发(workflow_dispatch):

| 分支 | 推送地址 |
|------|----------|
| main | `docker pull hub-harbor.oepkgs.net/oerv-ci/jenkins-agent-gitee:jdk17` |
| dev | `docker pull hub-harbor.oepkgs.net/oerv-ci/jenkins-agent-gitee:jdk17-dev` |

### 配置说明

1. 在仓库 Settings -> Secrets and variables -> Actions 中配置 Harbor 凭据:变量(Variables) `DOCKERHUB_OEPKGS_OERVCI_USERNAME`、密钥(Secrets) `DOCKERHUB_OEPKGS_OERVCI_TOKEN`,其余 Secret 详见 workflow 文件头部注释.
2. 镜像为 riscv64 架构,默认在 GitHub 托管 runner 上通过 QEMU 模拟构建,较慢.