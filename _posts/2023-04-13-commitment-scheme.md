---
layout: post
title:  "Commitment scheme security"
categories: jekyll update
usemathjax: true
---

We prove that $\Gamma$ is a perfectly binding and computationally hiding commitment scheme.

### Lemma 12 (Perfectly binding)

The commitment scheme $\Gamma$ is perfectly binding.

*Proof:* Recall that the decryption key $r = r_{i}^{k} + r_{i}^{p}$ for each block $C_{i}$ is secret-shared across both $C$ and $V$. The authenticity of $C_{i}$ is assured to both parties by checking the tag of $C_{i}$ in 2PC. Then, as $C$ commits to both $C_{i}$ and $r_{i}^{p}$ before learning $r_{i}^{v}$, AES-GCM acts as a committing AEAD scheme from the perspective of $V$. $(C_{i}, k_{i}^{p})$ acts as a perfectly binding commitment to $M_{i}$.

### Lemma 13 (Computationally binding)

The commitment scheme $\Gamma$ is computationally hiding.

*Proof:* The client commitment is series of AES-GCM encrypted ciphertexts, for which $V$ only holds the key shares $(tk_{capp}^v,tk_{sapp}^v)$. Note that the full keys are defined as $(tk_{capp},tk_{sapp}) = (tk_{capp}^p \oplus tk_{capp}^v, tk_{sapp}^p \oplus tk_{sapp}^v)$. By the semantic security of the encryption scheme, we know that if the client generates two separate commitments using the same secret parameters, the encryptions of both will be indistinguishable with anything other than negligible probability. Therefore, the scheme is computationally binding for all bounded adversaries.
