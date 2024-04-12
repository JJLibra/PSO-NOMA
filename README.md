# 📨 PSO-NOMA

Design and implementation of secure NOMA transmission based on PSO algorithm

## 📄 Background

Power domain NOMA (non-orthogonal multiple access) is an efficient access method. Multiple users achieve superimposed transmission by using different transmit powers. The receiving end uses a detection algorithm based on signal-to-interference-to-noise ratio and continuous interference cancellation. Iteratively recover data. Based on the NOMA transmission mechanism, how to ensure safe transmission for users?

## 💡 Ideas

Select an anti-eavesdropping user from the NOMA user group as a Jammer (jammer), and ensure that the sum of user security capacities is maximized by reasonably allocating the NOMA user's power (including Jammer's power). Essentially, the NOMA security capacity maximization problem is constructed and solved using the PSO algorithm.