---
pip: 26
title: Minimum Availability Score
author: B00f (@b00f)
status: Final
discussion-no: 120
type: Standards Track
category: Core
created: 09-06-2024
---

## Abstract

This proposal suggests setting the Minimum Availability Score to 0.666667 for validators in the Pactus network.
This score ensures that validators who fail to meet this threshold cannot propose a block,
thereby maintaining the network's stability and reliability.

## Motivation

Based on PIP-19 [^1], validators with an Availability Score below the Minimum Availability Score cannot propose blocks.
Therefore, it is essential to set a fair and effective minimum threshold to ensure network performance and security.

## Specification

The Availability Score ($S_i$) is calculated by dividing the number of blocks that a validator has signed ($V_i$)
by the number of times a validator could sign a block ($N_i$):

$$
S_i = \frac{V_i}{N_i}
$$

When a block is created, non-faulty validators should include all the signatures they receive in the block certificate.
However, faulty validators may fail to do so, either intentionally or unintentionally.

Let's assume a worst-case scenario where up to 1/3 of validators may be faulty
(e.g., due to poor internet connections, unsynchronized clock, selfish behavior, etc.).
As a result, a validator's signature might only be included in 2/3 of the blocks they are supposed to sign:

$$
V_i = \frac{2}{3} \times N_i
$$

Therefore, the Minimum Availability Score $S_{min}$ is calculated as:

$$
S_{min} = \frac{\frac{2}{3} \times N_i}{N_i} = \frac{2}{3} \approx 0.666667
$$

## Backward Compatibility

Once the majority of nodes adopt this number, validators with lower scores will no longer receive rewards.

## Security Considerations

This proposal should improve the security of the protocol,
as validators will tend to monitor their nodes to avoid falling below the minimum threshold.

## References

[^1]: [PIP-19 - Availability Score for Validators](https://pips.pactus.org/PIPs/pip-19)
