Question: Finite Horizon Policies

- Set \( k = 1 \)  

- Initialize \( V_0(s) = 0 \) for all states \( s \)  

- Loop until \( k == H \):  

  - For each state \( s \)  
    $$
     V_{k + 1}(s) = \max_a R(s, a) + \gamma \sum_{s' \in S} P(s'|s, a) V_k(s')
    $$
    

  - $$
    \pi_{k + 1}(s) = \arg\max_a R(s, a) + \gamma \sum_{s' \in S} P(s'|s, a) V_k(s')
    $$

Is optimal policy stationary (independent of time step) in finite horizon tasks?

我感觉我不理解问题的 含义： 什么叫和时间步独立呢？

> **stationary policy（平稳策略）**：
>  指的是策略只依赖于当前状态，不依赖于时间步。也就是说，无论是在第1步、第10步还是第100步，只要到了状态s，采取的动作都一样

在有限时域的任务里；也就是说 时间步的长短不会影响我的最终搜索到的最优策略；是的 ，策略优化在有限域内可以不等agent走任意一步就计算出最优策略。但是最终执行肯定还是需要和时间步相关，如果时间步太短，无法收敛到最优。设t0 = 从最差state 到最优state end 的时间，则t > t0时，该策略与时间步独立。

- Define MP, MRP, MDP, Bellman operator, contraction, model, Q-value, policy  
- Be able to implement  
  - Value Iteration  (值迭代：根据贝尔曼方程每次都计算最好的奖励值函数的状态)
  - Policy Iteration  （使用Q函数，进行当前动作奖励+ 未来旧策略下的价值的迭代）
- Give pros and cons of different policy evaluation approaches  
- Be able to prove contraction properties  
- Limitations of presented approaches and Markov assumptions  
  - Which policy evaluation methods require the Markov assumption?

1 MP： 马尔可夫过程； 当前状态仅受上一个状态影响；
2 MRP：马尔可夫过程奖励：当前奖励仅受上一个状态奖励的影响

3 MDP： 马尔可夫决策过程： 在马尔可夫状态下选择策略的过程。

4  Bellman operator：某种算子；在这里特指Bellman方程对价值函数的变换过程
5 contraction：缩放

6 model： 奖励模型，数学模型等

7  Q-value： 当前动作奖励+ 未来旧策略下的价值

8 policy：执行动作的某种策略

Be able to prove contraction properties  ：这里只需要写下

 |BVk - BVj| =max a - max b < = max (a - b )后面的约掉奖励，第二个不等式使用

W1 max1 +w2 max2  < = Max.        (w1+w2 = 1;Max >= max1, max2 )

Give pros and cons of different policy evaluation approaches  ：我理解的策略迭代可以永远保证优化单调；值迭代则由缩放因子保证值差越来越小，换句话说类似某种梯度下降的方式。他们的优点和缺点一致：可以探索全局最优，但是资源消耗较大（比深度遍历efficient），在实践过程中需要设置有限的视野。

Limitations of presented approaches and Markov assumptions  

- Which policy evaluation methods require the Markov assumption?这个问题我不会，请你帮我解决 

Markov Assumption（马尔可夫性假设）相关
Which policy evaluation methods require the Markov assumption?
值迭代（Value Iteration）/ 策略迭代（Policy Iteration）/ Bellman方程本身：都需要马尔可夫性假设。
因为贝尔曼方程的前提是“下一个状态和奖励只依赖当前状态和动作”，不依赖历史。
没有马尔可夫性，贝尔曼递推公式不成立。
采样-平均法（如蒙特卡洛估计）：不需要马尔可夫性。只要能采集轨迹就能估计平均回报。