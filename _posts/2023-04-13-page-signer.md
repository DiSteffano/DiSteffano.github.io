---
layout: post
title:  "Page Signer and AES-GCM"
categories: jekyll update
usemathjax: true
---

We compare our approach to computing AES-GCM tags to the approach employed by PageSigner [\[1\]](#references).
In a 2PC setting, we assume that both $k$ and the powers of $h = h_{p} + h_{v}$ are additively shared by both parties, with $C$, $IV$ and $A$ acting as public inputs.

Assuming that $C$ is a single block without any associated data (i.e. $C = C_{1}$), we have $\tau = (h_{p}^{m-2} + h_{v}^{m-2}) \cdot (h_{p}^{1} + h_{v}^{1}) \cdot C_{1} = (h_{p}^{m-1} + h_{v}^{m-1} + h_{p}^{m-2} \cdot h_{v}^{1} + h_{v}^{m-2} \cdot h_{p}^{m-2}) \cdot C_{1}$. As the first of these terms can be computed locally, the cost of computing $\tau$ can be reduced to computing $(h_{v}^{m-2} \cdot h_{p} + h_{p}^{m-2} \cdot h_{v}) \cdot C_{1}$ in 2PC. This approach can actually be written as a variant of our approach, as the left hand-side is fixed for a particular sharing of $h$. However, PageSigner instead repeats this process each time a tag is computed. Interestingly, it turns out that simply computing a sharing of $h_{v}^{2}h_{p}$ and $h_{p}^{2}h_{v}$ is sufficient to tag blocks of arbitrary length, lowering the cost of tagging to just two OT-based multiplications.

From a performance perspective, a "back-of-an-envelope" calculation shows that this approach is strictly less performant than the approach used by us. Intuitively, this is because our approach allows all polynomial evaluation to be done locally, which is not the case for PageSigner: whilst both approaches require computing an initial sharing of $h$ and its powers, PageSigner's approach also requires computing two OT-based multiplications per tagging. Concretely, instantiating these multiplications using the maliciously secure scheme presented in [\[2\]](#references) with 128-bits of statistical security would require 2048 oblivious transfers of 128-bits for the multiplication alone, requiring around 32KiB of bandwidth per tag. In contrast, our scheme only requires transferring around 64 bytes per tagging operation. In other words, our scheme requires around 500xtimes less bandwidth per tagging operation than the approach employed by PageSigner.

## References

1. P. team, "Pagesigner: One-click website auditing" website, accessed 04/04/2023. [Online]. Available: [https://old.tlsnotary.org/pagesigner](https://old.tlsnotary.org/pagesigner).
2. J. Doerner, Y. Kondi, E. Lee, and a. shelat, "Secure two-party threshold ECDSA from ECDSA assumptions" in *2018 IEEE Symposium on Security and Privacy*. IEEE Computer Society Press, May 2018, pp. 980–997.
