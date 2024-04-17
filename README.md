## 📨 PSO-NOMA

Design and implementation of secure NOMA transmission based on PSO algorithm
What is designed is an uplink NOMA secure transmission scheme.

### 📄 Background

Power domain NOMA (non-orthogonal multiple access) is an efficient access method. Multiple users achieve superimposed transmission by using different transmit powers. The receiving end uses a detection algorithm based on signal-to-interference-to-noise ratio and continuous interference cancellation.
Iteratively recover data. Based on the NOMA transmission mechanism, how to ensure safe transmission for users?

### 💡 Key steps for upward NOMA

- Power distribution

     In uplink NOMA, different users are assigned different power levels according to their channel conditions (such as the distance between the user and the base station, channel quality, etc.). Generally speaking, users with poorer channel conditions (such as users farther away from the base station) will be allocated higher power, while users with better channel conditions (such as users closer to the base station) will be allocated lower power. . The purpose of this is to enable the base station to effectively distinguish and decode superimposed signals from different users.

- Signal transmission and superposition

     All users transmit their signals at approximately the same time. Since users are using the same frequency band, these signals will overlap in the air as they reach the base station. Therefore, the base station receives a superimposed signal that contains information from all users.

- Signal detection and decoding

     The base station uses a technology called Successive Interference Cancellation (SIC) to decode the superimposed signal. Specific steps are as follows:
     The signal of the user with the highest power (and usually the worst channel conditions) is decoded first.
     Once this signal is successfully decoded, its contribution is subtracted from the superimposed signal.
     Then the user signals at the next power level are decoded, and this process is repeated until all user signals are decoded.

- Performance optimization:

     Effective use of power distribution and SIC technology is the key to NOMA performance optimization. Proper power allocation ensures efficient signal decoding, while effective SIC implementation minimizes decoding errors and system complexity.

### 🤔 Ideas

Select an anti-eavesdropping user from the NOMA user group as a Jammer (jammer), and ensure that the sum of user security capacities is maximized by reasonably allocating the NOMA user's power (including Jammer's power). Essentially, the NOMA security capacity maximization problem is constructed and solved using the PSO algorithm.

The core advantage of NOMA is to improve spectrum efficiency and system capacity, especially when the number of users is large.

### 仿真应用场景

通过引入一个反窃听用户作为Jammer来增加通信的安全性，在每个簇中配置三个用户，其中一个用户将充当干扰机（Jammer）的角色。

#### 用户簇配置：

- **簇1：混合需求用户组（城市中心和近郊）**
  - **用户1**（高需求数据用户）：
    - 地理位置距离基站：100 m
    - 设备天线增益：15 dBi
    - 需求数据率：10 Mbps
    - 信道增益：-100 dB
  - **用户2**（中等需求数据用户）：
    - 地理位置距离基站：200 m
    - 设备天线增益：12 dBi
    - 需求数据率：5 Mbps
    - 信道增益：-110 dB
  - **用户3**（Jammer）：
    - 地理位置距离基站：150 m
    - 设备天线增益：13 dBi
    - 需求数据率：不适用（作为干扰源）
    - 信道增益：-105 dB

- **簇2：远距离用户组（郊区和偏远地区）**
  - **用户4**（中等需求数据用户）：
    - 地理位置距离基站：500 m
    - 设备天线增益：10 dBi
    - 需求数据率：3 Mbps
    - 信道增益：-120 dB
  - **用户5**（低需求数据用户）：
    - 地理位置距离基站：700 m
    - 设备天线增益：20 dBi
    - 需求数据率：1 Mbps
    - 信道增益：-130 dB
  - **用户6**（Jammer）：
    - 地理位置距离基站：550 m
    - 设备天线增益：11 dBi
    - 需求数据率：不适用（作为干扰源）
    - 信道增益：-125 dB

#### 系统参数和目标：

- 卫星下行链路总功率：25 Watts
- 噪声功率谱密度：-174 dBm/Hz
- 系统带宽：20 MHz
- 路径损耗模型：自由空间路径损失模型
- 功率分配目标：最大化系统的安全容量，同时保持每个非Jammer用户的需求数据率得到满足。

#### PSO算法配置：

- 粒子数：40
- 最大迭代次数：150
- 惯性权重（w）：0.7
- 个体学习因子（c1）：2.0
- 社会学习因子（c2）：2.0
- 速度限制：[-1, 1] 倍的功率范围

### 研究方法：

1. **初始化**：
   - 为每个用户随机分配初始功率，包括Jammer。
2. **评估**：
   - 计算当前功率分配下的系统安全容量，同时确保非Jammer用户的数据需求得到满足。
3. **更新**：
   - 根据PSO算法更新每个粒子的位置和速度。
4. **迭代**：
   - 重复评估和更新步骤，直到达到最大迭代次数或找到满意的解。

这种场景设计考虑了安全通信的需求，并且引入了干扰机的概念，增强了系统的安全性。通过PSO算法优化，您可以研究不同功率分配策略对系统安全容量的影响。




