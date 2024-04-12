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

### 🎉 initial plan

The core advantage of NOMA is to improve spectrum efficiency and system capacity, especially when the number of users is large.

Downloading......


