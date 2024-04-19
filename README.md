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
    - 信道增益：-105 dB
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
    - 信道增益：-115 dB
  - **用户5**（低需求数据用户）：
    - 地理位置距离基站：700 m
    - 设备天线增益：20 dBi
    - 需求数据率：1 Mbps
    - 信道增益：-120 dB
  - **用户6**（Jammer）：
    - 地理位置距离基站：550 m
    - 设备天线增益：11 dBi
    - 需求数据率：不适用（作为干扰源）
    - 信道增益：-125 dB

#### 系统参数和目标：

- 卫星下行链路总功率：15-40 Watts
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

#### 1. 定义优化变量

在这个问题中，每个粒子的位置向量代表一种功率分配方案。对于六个用户，包括两个干扰源，向量可能看起来像这样：

\[ P = [p_1, p_2, p_3, p_4, p_5, p_6] \]

其中 \( p_i \) 是第 \( i \) 个用户的功率分配，\( p_3 \) 和 \( p_6 \) 分别是簇1和簇2中的干扰机分配的功率。

#### 2. 设计目标函数

目标函数应该反映出您希望优化的指标——在这个场景中，是最大化上行NOMA系统的安全容量。安全容量可以根据每个用户的信号干扰加噪声比（SINR）和安全传输需求计算得出。具体地，您可以这样计算：

\[ C_i = \log_2(1 + \text{SINR}_i) \]

对于不作为干扰机的用户，\(\text{SINR}_i\) 可以这样计算：

\[ \text{SINR}_i = \frac{p_i h_i}{\sum_{j \neq i} p_j h_j + \sigma^2} \]

对于干扰机（Jammer），它们的功率分配会直接影响其他用户的SINR。

目标函数是所有非干扰机用户的安全容量之和，即：

\[ \text{maximize} \sum_{i \in \text{users, } i \neq \text{jammers}} C_i \]

#### 3. 约束条件

- **功率约束**：所有用户的功率总和不能超过总功率，即：

\[ \sum_{i=1}^6 p_i \leq P_{\text{total}} \]

- **功率非负性约束**：

\[ p_i \geq 0, \forall i \]

- **最小数据速率要求**：对于每个非干扰机用户，他们的数据速率必须满足最低需求，这可以通过他们的SINR来确保。

#### 4. PSO算法实现

- **初始化**：随机生成一定数量的粒子，每个粒子包含一组功率分配 \( P \)。
- **迭代优化**：
  - 对每个粒子，计算其目标函数值。
  - 更新每个粒子的个体最优和全局最优。
  - 更新粒子的速度和位置。
- **终止条件**：当达到最大迭代次数或全局最优在一定迭代内没有显著改进时停止。

#### 5. 分析和验证

- 分析最终的功率分配方案是否符合所有约束条件。
- 验证该方案是否真正达到了预期的最大安全容量。

> 仿真场景中，位置距离、天线增益、需求数据率、信道增益等参数对于设计和优化非正交多址接入（NOMA）系统中的功率分配具有重要的作用。下面详细解释每个参数的用途和它们在功率分配以及PSO算法中的重要性：

#### 1. 位置距离（Distance from Base Station）

位置距离影响信号传播的衰减。在卫星或通信系统中，信号衰减通常与距离的平方或更高次幂成正比（根据自由空间路径损失模型或其他更复杂的传播模型）。因此，距离信息用来计算信道增益或路径损失，影响到功率分配策略的设计。

#### 2. 天线增益（Antenna Gain）

天线增益描述了天线集中信号能量的能力。高增益天线能更有效地发送和接收远距离信号，减少所需的传输功率或提高接收信号的质量。在功率分配中，天线增益直接影响到所需的最小功率水平，以保证足够的信号质量。

#### 3. 需求数据率（Required Data Rate）

每个用户的需求数据率定义了他们的服务质量需求（QoS）。在设计功率分配策略时，必须确保每个用户至少获得其需求的数据率，这是功率分配的基本约束条件之一。这直接关系到用户的满意度和系统的性能评价。

#### 4. 信道增益（Channel Gain）

信道增益反映了用户与基站之间的信号衰减程度，可能包括路径损失、阴影衰落和多径衰落等因素。这是评估每个用户SINR的关键参数，进而影响数据传输的可靠性和速率。在计算每个用户的SINR时，需要考虑信道增益、分配的功率以及其他用户的干扰。

#### 将这些参数整合应用到PSO算法：

- **信道模型构建**：基于位置距离和信道增益，构建每个用户的信道衰减模型。
- **功率分配的目标函数**：利用天线增益和信道增益计算每个用户的接收功率，进而计算SINR和数据率，以确保每个用户的需求数据率得到满足。
- **优化过程**：通过PSO算法搜索功率分配的最优解，使得系统的总体性能最优化，如最大化总数据率或最大化安全容量，同时考虑到每个用户的服务质量需求。

通过对这些参数的精确计算和合理应用，可以有效地设计出一个既考虑实际通信环境又满足用户需求的功率分配策略。这不仅提高了系统的效率，还能保障用户体验和系统的公平性。


