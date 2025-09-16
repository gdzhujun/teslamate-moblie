# TeslaMate Mobile

**一款非官方的移动客户端，旨在为您提供便捷的方式来查看和交互您的 TeslaMate 数据。随时随地监控您的特斯拉车辆状态、行程、充电等信息。**

---

## 目录

- ✨ 主要功能
- 📸 应用截图
- ⚙️ 配置您的 TeslaMate API
- 🙏 致谢

---

## ✨ 主要功能

*   **实时车辆状态**:
    *   查看当前电池电量 🔋
    *   预估剩余里程🛣️
    *   车辆固件版本
    *   当前里程表读数
    *   显示车辆过往状态的时间轴
*   **行程记录 (Drives)**:
    *   浏览历史行程列表
    *   查看每个行程的详细信息：
        *   起止时间、地点
        *   行驶距离、时长
        *   平均速度、最高速度
        *   能耗、效率
        *   室外温度
    *   行程轨迹地图展示 🗺️
    *   行程相关的图表分析 (速度、功率、海拔、温度、胎压)
*   **充电记录 (Charges)**:
    *   浏览历史充电会话列表
    *   查看每次充电的详细信息：
        *   开始/结束时间、地点
        *   充电量 (kWh)、充电时长
        *   充电功率、电压、电流等图表 📊
        *   充电类型 (AC/DC)
*   **电池健康度 (Battery Health)**:
    *   查看电池健康百分比
    *   新车可用电量 vs 当前可用电量
    *   新车最大续航 vs 当前最大续航
    *   容量衰减和续航损失估算
*   **统计与概览 (Statistics / Overview - 根据您的实现情况)**:
    *   总行驶里程
    *   总能耗
    *   每日/每月行驶里程图表
    *   驾驶次数统计
    *   [您可以在此添加更多统计功能]
*   **位置服务**:
    *   查看常去地点 (Visited locations)
    *   终身驾驶地图 (Lifetime drive map)
*   **车辆更新 (Updates)**:
    *   查看车辆软件更新历史
*   **用户设置**:
    *   配置连接到您自己的 TeslaMate API 服务器地址和 Token
    *   时区设置
    *   单位设置 (公里/英里)
    *   夜间/深色模式切换 🌃
    *   测试数据库连接功能 📡

---

## 📸 应用截图
<img width="540" height="1200" alt="Screenshot_20250916_154354" src="https://github.com/user-attachments/assets/31538a48-c967-4c73-8a65-06b5f0a2573c" />
<img width="540" height="1200" alt="Screenshot_20250916_154345" src="https://github.com/user-attachments/assets/67cb19ff-5551-43f4-9212-48518591d201" />
<img width="540" height="1200" alt="Screenshot_20250916_154326" src="https://github.com/user-attachments/assets/9235a35d-d80e-42a4-9c78-c75c2dca05d7" />
<img width="540" height="1200" alt="Screenshot_20250916_154312" src="https://github.com/user-attachments/assets/43ae4b54-be0b-4b7a-9a64-e09d84a24606" />
<img width="540" height="1200" alt="Screenshot_20250916_154300" src="https://github.com/user-attachments/assets/ce885a6d-35a3-429a-8378-a2acd6bbd18f" />
<img width="540" height="1200" alt="Screenshot_20250916_154245" src="https://github.com/user-attachments/assets/c3be9d32-cedd-4a12-a976-5d08a53c7d9c" />
<img width="540" height="1200" alt="Screenshot_20250916_154235" src="https://github.com/user-attachments/assets/16853d2d-1656-4790-b81a-99f696486646" />
<img width="540" height="1200" alt="Screenshot_20250916_154136" src="https://github.com/user-attachments/assets/ac7a7df1-13c5-4adb-b5f5-7010ded2ba46" />
<img width="540" height="1200" alt="Screenshot_20250916_154047" src="https://github.com/user-attachments/assets/723ba51c-e818-4b33-9443-67e2d98268e9" />
<img width="540" height="1200" alt="Screenshot_20250916_154038" src="https://github.com/user-attachments/assets/ff9f2d7b-b51e-46a8-bc9d-0f4eb55cd356" />
<img width="540" height="1200" alt="Screenshot_20250916_154021" src="https://github.com/user-attachments/assets/b049900a-d665-4e78-b875-6f4d721e22c0" />
<img width="540" height="1200" alt="Screenshot_20250916_154009" src="https://github.com/user-attachments/assets/d9352e56-275c-468a-8397-890f6e579108" />
<img width="540" height="1200" alt="Screenshot_20250916_153839" src="https://github.com/user-attachments/assets/4d683ff7-ff25-4b84-93b6-5a8d555f43ea" />

## ⚙️ 配置您的 TeslaMate API
### 前提条件
您需要已经通过 Docker 成功部署了 [TeslaMate](https://github.com/teslamate-org/teslamate)。本服务的数据库将连接到您现有的 
TeslaMate 数据库。

---

### 服务端安装

您可以通过以下任一方式安装 `tmate-api` 服务端：

1. 使用 Docker Compose (docker-compose.yml)将以下服务配置添加到之前您部署teslamate时的 docker-compose.yml 文件中的 services 部分：

```
services:
  #您现有的服务配置

  # 添加 tmate-api 服务
  tmate-api:
    image: gdzhujun933/tmate-api:latest
    container_name: tmate-api
    restart: unless-stopped
    environment:
      - DB_HOST=database
      - DB_PORT=5432        # 与teslamate相同，默认5432
      - DB_NAME=teslamate        # 与teslamate相同
      - DB_USER=teslamate        # 与teslamate相同
      - DB_PASS=your_teslamate_db_password    # 必须与teslamate设置的完全相同
      - API_KEY=your_secret_api_key_here             # 自行设置，后续app中需要填入
    ports:
      - "9999:8080"  # 可修改为其他端口
````

#### 2. 使用 Docker `run` 命令快速部署

```
docker run -d \
--name tmate-api \
--network docker_default \  #重要参数不能乱填，否则导致与teslamate不在一个网络内无法连上数据库
-p 9999:8080 \
--restart unless-stopped \
-e DB_HOST=database \
-e DB_PORT=5432 \
-e DB_NAME=teslamate \
-e DB_USER=teslamate \
-e DB_PASS=your_teslamate_db_password \
-e API_KEY=your_secret_api_key_here \
gdzhujun933/tmate-api:latest
```


**重要环境变量说明：**

*   `network`:填之前用docker network ls命令查看当前的网络清单，以ubuntu为例，查询结果是：
*   root@teslamate:/home/ubuntu# docker network ls
NETWORK ID     NAME             DRIVER    SCOPE
acfe0f8b26af   bridge           bridge    local
9097dde69d15   host             host      local
0b43f3509fc9   none             null      local
fa48b522c33c   ubuntu_default   bridge    local
* 那就应该改成--network ubuntu_default
*   `DB_PASS`: **必须**与您部署 TeslaMate 时为数据库设置的 `POSTGRES_PASSWORD` 
或 `DATABASE_PASS` 完全相同。
*   `API_KEY`: 您自定义的 API 
密钥（Token）。后续在 App 
的设置中需要填入此值以进行验证。



**注意：**

*   `--network docker_default`: 确保此服务与您的 TeslaMate `database` 
容器在同一个 Docker 
网络中，以便能够通过服务名 `database` 访问数据库。如果您的 TeslaMate 
使用了不同的网络名称，请替换 `docker_default`。
*   `-p 9999:8080`: 将宿主机的 `9999` 端口映射到容器的 `8080` 
端口。您可以根据需要修改宿主机端口 `9999`。
*   将 `your_teslamate_db_password` 替换为您的 TeslaMate 数据库密码。
*   将 `your_secret_api_key_here` 替换为您自定义的 API 密钥。

---
## App 配置

安装完 App 后，您需要在 App 的**设置**中填写以下信息才能正常使用：

1.  **服务器地址 (Server Address):**
    *   格式为：`http://<您的服务器IP或域名>:<端口号>`
    *   例如，如果 `tmate-api` 服务部署在 IP 地址为 `10.0.0.234` 的服务器上，并且您在 Docker 
部署时将宿主机端口设置为 `9999`，则服务器地址应填写为：`http://10.0.0.234:9999`
2.  **Token:**
    *   填写您在部署服务端时设置的 `API_KEY` 的值。

---



注意：•确保 DB_HOST 指向的是您 Docker Compose 文件中定义的 TeslaMate 数据库服务的名称（通常是 database）。•将 your_teslamate_db_password 替换为您的 TeslaMate 数据库密码。•将 your_secret_api_key_here 替换为您自定义的 API 密钥。•如果您的 TeslaMate 服务使用了自定义的 Docker 网络，请确保 tmate-api 服务也通过 networks 指令连接到相同的网络。

## 🙏 致谢
感谢 TeslaMate 项目的创建者和贡献者，为我们提供了如此强大的特斯拉车辆数据记录平台。

    
