# RAGFlow v0.25.6 纯原生 ARM64 Docker 镜像 + GPU 显卡加速部署方案

🚀 **专为国内 ARM64 架构服务器/工作站（如 NVIDIA DGX Spark、Grace CPU、飞腾、鲲鹏等标准 ARM64 算力设备）定制的离线一键起飞全家桶！**

## 💡 为什么需要本项目？
1. **官方痛点**：RAGFlow 官方目前不维护原生 ARM64 架构的 Docker 镜像。
2. **编译黑洞**：如果直接在 ARM 机器上通过官方源码编译，在 `uv pip install` 阶段会因为跨架构转译（QEMU）导致 CPU 占用率归零，发生长时间无预警僵死。
3. **网络死锁**：国内直接拉取 Docker Hub 或 GHCR 镜像经常超时报错。

**本项目直接提供在英伟达 DGX Spark (Grace CPU) 顶级工作站上硬核编译通过的 7.8GB 业务完全体镜像！配合 123 云盘不限速下载，解密国内 ARM 部署的终极速度。**

> ⚠️ **关于华为昇腾（Ascend NPU）的兼容性说明**：
> 本镜像是基于英伟达 CUDA 显卡加速环境编译。若使用华为昇腾等 NPU 设备，**不支持**直接运行本镜像。推荐采用“混合架构”：使用本镜像在 ARM/NVIDIA 节点上进行文档解析与知识库管理，大模型推理则由昇腾节点（通过 vLLM-Ascend 或 MindIE）吐出兼容 OpenAI 的 API 接口，在 RAGFlow 后台一键接入联动。

---

## 📦 第一步：核心大件下载（7.8 GB 离线镜像包）

请通过以下国内高速云盘链接，下载编译好的纯原生 ARM64 业务镜像压缩包：

* **🔥 123云盘高速下载链接**：[👉 https://1817027392.share.123pan.cn/123pan/Ye3VVv-xOiYA?pwd=VZBG# 👈]

下载完成后，将 `ragflow_v0.25.6_arm64.tar` 文件上传到你的服务器，并在当前目录下执行以下命令导入镜像：
```bash
docker load -i ragflow_v0.25.6_arm64.tar




ragflow-arm64-gpu-dgx-spark/
├── .env                  # 你改好的完美环境变量配置
├── docker-compose.yml    # 容器编排主图纸
├── README.md             # 刚写好的保姆级大圣经
└── nginx/                # 🚀 必须带上这个：前端反向代理配置文件夹
    └── ragflow.conf      # 核心：Nginx 路由配置文件
