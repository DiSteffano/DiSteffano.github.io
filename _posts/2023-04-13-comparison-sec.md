---
layout: post
title:  "Comparison with prior security models"
categories: jekyll update
usemathjax: true
---

## DECO protocol [\[1\]](#references)

In [\[1\]](#references), the authors consider an all-encompassing simulation-based (i.e. real-ideal-world) security model, that includes the client proving knowledge of facts associated with the commitment $c_{\hat{q}, \hat{r}}$. This approach has a number of downsides. As stated previously, it does not apply when handshakes are performed using TLS 1.3, and formal guidance is not given on how to adapt their security proof to this case. Moreover, their ideal-world functionality does not establish a number of security properties that have later been shown to be guaranteed by the TLS 1.3 protocol [\[2\]](#references). Furthermore, the identity of the TLS server is known to $V$, which contradicts one of the security properties that we aim to achieve. In summary, their proof is not modular, and so making changes to their model to incorporate these changes would be a significant task.

## Oblivious TLS [\[3\]](#references) and N-for-1-Auth [\[4\]](#references)

In both [\[3\]](#references) and [\[4\]](#references), $C$ and/or $S$ are built as a series of entities, combining to execute the given role in the TLS handshake as an MPC functionality or *TLS engine*. In [\[3\]](#references), the authors show that the security of the TLS exchange in the multi-stage key exchange security model of [\[2\]](#references) can be maintained, with some tweaks that allow the TLS engines to reveal all secret material, when a single party is corrupted. In [\[4\]](#references), a security model that is similar to the approach of [\[1\]](#references) is achieved, by modelling the handshake and record-layer protocols as an ideal functionality, and using the real-ideal-world paradigm to prove security.

Note that both protocols assume that all parties learn the same information (except for a single party that relays the eventual TLS messages between the engine and the other entity). Moreover, their model does not take into account security guarantees that are only made explicit when the client attempts to attest to data that was exchanged in the TLS connection. However, the security model of Oblivious TLS is useful to us, as it allows for proving that a multi-party client can achieve a TLS~1.3 handshake with the security guarantees established in [\[2\]](#references). We adapt this to work in our scenario, so that we can provide similar guarantees.

## References

1. F. Zhang, D. Maram, H. Malvai, S. Goldfeder, and A. Juels, "DECO: Liberating web data using decentralized oracles for TLS" in *ACM CCS 2020*, J. Ligatti, X. Ou, J. Katz, and G. Vigna, Eds. ACM Press, Nov. 2020, pp. 1919–1938.
2. B. Dowling, M. Fischlin, F. G¨unther, and D. Stebila, "A cryptographic analysis of the TLS 1.3 handshake protocol", *Journal of Cryptology*, vol. 34, no. 4, p. 37, Oct. 2021.
3. D. Abram, I. Damgård, P. Scholl, and S. Trieflinger, "Oblivious TLS via multi-party computation" in *CT-RSA 2021*, ser. LNCS, K. G. Paterson, Ed., vol. 12704. Springer, Heidelberg, May 2021, pp. 51–74.
4. W. Chen, R. Deng, and R. A. Popa, "N-for-1 auth: N-wise decentralized authentication via one authentication", *Cryptology ePrint Archive*, Report 2021/342, 2021, [https://eprint.iacr.org/2021/342](https://eprint.iacr.org/2021/342).
