DQN
===

- Using Q network to be a proxy of Q function
- replay buffer: a batch of tuples of (s, a, s', r, d) [where d is the terminal flag]
- we need to create the datasets with X & Y for training a Q network
  - X: we will use a initialized Q network to play the game, many times, with ϵ-greedy. Then the rollouts would be saved as replay buffer.
  Then we will use the (s, a, s', r) as the X
  - Y: y = r + γ Q(phi(s'), a')
