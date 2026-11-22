# A Tight 52/75 Exponent for a Two-Schedule Contraction Bound in Set-Multilinear PIT

**Research note — 23 November 2026**  
**Status:** conditional algorithmic result; central optimization lemma is proved below.  
**Author:** to be completed by the submitting author.

## Abstract

We study a modification of the coefficient-inner-product stage in deterministic polynomial identity testing (PIT) for syntactically set-multilinear arithmetic circuits over the integers. The modification uses a rectangular matrix-multiplication bound

\[
\omega(1,2,1)\leq \frac{25}{8}
\]

to accelerate the two natural contraction orders arising from the heavy-gate decomposition. The relevant dimension parameters reduce to four nonnegative reals \(a,b,c,e\) satisfying

\[
a+b+c+e=d,\qquad a+b,\ a+c,\ b+e,\ c+e\geq d/3.
\]

For the two contraction schedules, we prove that the better schedule has arithmetic-operation exponent at most

\[
\frac{52}{75}d+\varepsilon d+o(d).
\]

The constant \(52/75\) is sharp for this **two-schedule upper-bound model**: the normalized dimension vector \((a,b,c,e)=(9,16,16,34)d/75\) attains equality in the limiting optimization problem. We also explain how a fixed rational bilinear base scheme gives a polynomial bit-height overhead, and how the improved contraction bound can be inserted into the existing set-multilinear PIT framework.

The result is conditional on the rectangular matrix-multiplication exponent bound and on the exact rational implementation argument stated here. It does not prove a lower bound for unrestricted tensor contraction, does not produce a polynomial-time SAT algorithm, and does not resolve \(P\) versus \(NP\).

---

## 1. Scope and status of the result

The result has three logically distinct components.

1. **Optimization theorem.** A four-case inequality proves an exact minimax bound for two specified contraction schedules. This is an elementary theorem about a finite-dimensional feasible region.
2. **Algorithmic transfer.** The optimization theorem gives a faster upper bound for the inner-product computation in the heavy-decomposition PIT algorithm, provided the rectangular matrix-multiplication exponent can be realized by a fixed rational bilinear scheme with controlled coefficient height.
3. **Complexity-theoretic consequence.** If the preceding transfer is valid, the running-time parameter in the relevant PIT subroutine improves. The logical conclusion of the cited Boolean–arithmetic win–win theorem does not change.

The optimization lemma is a genuine mathematical result within the stated model. Its **literature novelty is not certified** by this note; a priority and related-work search is still required before describing it as a new published discovery. The end-to-end PIT theorem should be presented as conditional until the rational implementation and all algorithmic details have been independently checked or formalized.

## 2. Rectangular multiplication and the blocking bound

We use the rectangular exponent statement

\[
\omega(1,k,1)\leq
\begin{cases}
2,&0\leq k\leq 1/2,\\[1mm]
1+k+\dfrac{1}{4k},&k\geq 1/2.
\end{cases}
\]

At \(k=2\), this gives

\[
\omega(1,2,1)\leq 1+2+\frac18=\frac{25}{8}.
\]

Thus, for every fixed \(\eta>0\), the rectangular product

\[
N\times N^2\quad\text{by}\quad N^2\times N
\]

has an arithmetic-operation upper bound \(O_\eta(N^{25/8+\eta})\). The cited rectangular result states that its exponent bounds extend from \(\mathbb C\) to characteristic-zero fields by invariance of asymptotic tensor rank under field extension. The version located for this note is an arXiv preprint rather than a peer-reviewed journal publication. The preprint also discloses that its proof analysis and write-up were produced with OpenAI Codex; this does not establish that the mathematics is wrong, but it makes independent proof checking especially important.

Now consider

\[
A\in\mathbb{Q}^{m^p\times m^q},\qquad
B\in\mathbb{Q}^{m^q\times m^r}.
\]

Set

\[
w=\min\left(p,r,\frac q2\right).
\]

Partition the product into blocks of dimensions

\[
m^w\times m^{2w},\qquad m^{2w}\times m^w.
\]

The number of block products is at most

\[
m^{p-w}\,m^{q-2w}\,m^{r-w}=m^{p+q+r-4w}.
\]

Each block multiplication costs \(m^{(25/8+\eta)w+o(d)}\), so the total exponent is

\[
\begin{aligned}
p+q+r-4w+\left(\frac{25}{8}+\eta\right)w
&=p+q+r-\left(\frac78-\eta\right)w.
\end{aligned}
\]

Ignoring the arbitrarily small exponent slack for the optimization step, define

\[
\boxed{R(p,q,r)=p+q+r-\frac78\min\left(p,r,\frac q2\right).}
\]

The \(\eta\)-dependent loss is at most \(\eta d\) in the application below and is absorbed into the final \(\varepsilon d\) term.

## 3. The two contraction schedules

Consider the four-factor contraction

\[
I=\sum_{a,b,c,e}g[a,b]h'[b,e]h[c,e]g'[a,c],
\]

where

\[
a+b+c+e=d,
\qquad a+b,\ a+c,\ b+e,\ c+e\geq d/3.
\]

There are two natural ways to parenthesize this contraction.

### Schedule 1: contract over \(b\) and \(c\) first

Compute

\[
A[a,e]=\sum_b g[a,b]h'[b,e],\qquad
A'[a,e]=\sum_c g'[a,c]h[c,e],
\]

then compute

\[
I=\sum_{a,e}A[a,e]A'[a,e].
\]

### Schedule 2: contract over \(a\) and \(e\) first

Compute

\[
B[b,c]=\sum_a g[a,b]g'[a,c],\qquad
B'[b,c]=\sum_e h'[b,e]h[c,e],
\]

then compute

\[
I=\sum_{b,c}B[b,c]B'[b,c].
\]

Introduce the ordered dimension parameters

\[
u=\min(a,e),\quad U=\max(a,e),\qquad
v=\min(b,c),\quad V=\max(b,c).
\]

Then

\[
u+U+v+V=d,\qquad u\leq U,\quad v\leq V.
\]

The four cross-sum constraints are equivalent to

\[
\boxed{u+v\geq d/3.}
\]

For Schedule 1, the more expensive of the two rectangular products is the one using the larger of \(b,c\), namely \(V\). The final dot product is no more expensive than this bound. Its exponent is therefore at most \(d-L_1\), where

\[
L_1=v+\frac78\min\left(u,\frac V2\right).
\]

Similarly, Schedule 2 has exponent at most \(d-L_2\), where

\[
L_2=u+\frac78\min\left(v,\frac U2\right).
\]

Choosing the faster schedule gives the exponent bound

\[
E\leq d-\max(L_1,L_2).
\]

Consequently, the optimization problem is to find a lower bound for \(\max(L_1,L_2)\).

## 4. Exact optimization lemma

### Theorem 1 — Two-schedule savings bound

Let \(d\geq0\), and let \(u,U,v,V\geq0\) satisfy

\[
u\leq U,\qquad v\leq V,\qquad u+U+v+V=d,
\qquad u+v\geq d/3.
\]

Define

\[
L_1=v+\frac78\min\left(u,\frac V2\right),\qquad
L_2=u+\frac78\min\left(v,\frac U2\right).
\]

Then

\[
\boxed{\max(L_1,L_2)\geq\frac{23d}{75}.}
\]

### Proof

There are four cases, depending on the two comparisons \(u\leq V/2\) and \(v\leq U/2\).

**Case I: \(u\leq V/2\) and \(v\leq U/2\).**

Here

\[
L_1=v+\frac78u,\qquad L_2=u+\frac78v.
\]

Therefore

\[
L_1+L_2=\frac{15}{8}(u+v),
\]

and hence

\[
\max(L_1,L_2)\geq\frac{15}{16}(u+v)
\geq\frac{5d}{16}\geq\frac{23d}{75}.
\]

**Case II: \(u\geq V/2\) and \(v\geq U/2\).**

Now

\[
L_1=v+\frac{7}{16}V,\qquad
L_2=u+\frac{7}{16}U.
\]

Using \(U+V=d-(u+v)\),

\[
L_1+L_2
=u+v+\frac{7}{16}(U+V)
=\frac{7d}{16}+\frac{9}{16}(u+v).
\]

Since \(u+v\geq d/3\),

\[
\max(L_1,L_2)\geq\frac{L_1+L_2}{2}
\geq\frac{5d}{16}\geq\frac{23d}{75}.
\]

**Case III: \(u\leq V/2\) and \(v\geq U/2\).**

In this case,

\[
L_1=v+\frac78u,\qquad
L_2=u+\frac{7}{16}U.
\]

Take the convex combination

\[
\frac{23}{25}L_1+\frac{2}{25}L_2
=\frac{23}{25}v+\frac{177}{200}u+\frac{7}{200}U.
\]

Because \(U\geq u\),

\[
\frac{23}{25}L_1+\frac{2}{25}L_2
\geq\frac{23}{25}(u+v).
\]

A convex combination cannot exceed the maximum of its entries, so

\[
\max(L_1,L_2)
\geq\frac{23}{25}(u+v)
\geq\frac{23d}{75}.
\]

**Case IV: \(u\geq V/2\) and \(v\leq U/2\).**

This is symmetric to Case III. We have

\[
L_1=v+\frac{7}{16}V,\qquad
L_2=u+\frac78v.
\]

Using \(V\geq v\),

\[
\frac{2}{25}L_1+\frac{23}{25}L_2
\geq\frac{23}{25}(u+v)
\geq\frac{23d}{75}.
\]

Again, the left-hand side is a convex combination, so it is bounded above by \(\max(L_1,L_2)\). This proves the theorem. \(\square\)

### Corollary 1 — Exponent upper bound

For the faster of the two schedules,

\[
E\leq d-\frac{23d}{75}=\boxed{\frac{52d}{75}}.
\]

With the rectangular multiplication slack included, the conclusion is

\[
E\leq\left(\frac{52}{75}+\varepsilon\right)d+o(d)
\]

for every fixed \(\varepsilon>0\).

## 5. Tightness for this two-schedule estimate

Consider

\[
(a,b,c,e)=\frac d{75}(9,16,16,34).
\]

Then

\[
u=\frac{9d}{75},\quad U=\frac{34d}{75},\quad
v=V=\frac{16d}{75}.
\]

Consequently,

\[
L_1=\frac{16d}{75}+\frac78\frac{8d}{75}
=\frac{23d}{75},
\]

and

\[
L_2=\frac{9d}{75}+\frac78\frac{16d}{75}
=\frac{23d}{75}.
\]

Thus the lower bound in Theorem 1 is attained in the continuous feasible region. If strict integer inequalities are required, for \(d=75k\) one can take

\[
(a,b,c,e)=(9k+1,16k,16k,34k-1).
\]

For \(k\geq1\), this satisfies all four strict cross-sum constraints. In this case \(L_1=23k\), \(L_2=23k+1\), and the two-schedule exponent is \(52k-1\). Its ratio to \(d=75k\) tends to \(52/75\). Hence

\[
\boxed{\sup E=\frac{52d}{75}}
\]

for the specified two-schedule estimate.

**Interpretation:** this is not a lower bound on unrestricted tensor-contraction complexity. A different contraction schedule, a multiway contraction, or an algorithm exploiting additional structure may be faster.

## 6. Transfer to the set-multilinear PIT algorithm

The reference PIT algorithm decomposes the output polynomial as a sum of products

\[
f_\Phi=\sum_{\beta\in\mathcal F}g_\beta h_\beta
\]

and computes the squared coefficient norm by summing inner products

\[
\langle g_\beta h_\beta,g_{\beta'}h_{\beta'}\rangle.
\]

The two-schedule contraction above replaces the naive contraction used for each such pair.

There is an important preprocessing detail that should be stated explicitly. In the heavy decomposition:

- every non-heavy gate has type size at most \(2d/3\);
- each transfer polynomial \([\alpha:\beta]\) has type size below \(d/3\);
- each polynomial \(h_\beta\) has type size below \(2d/3\).

A coefficient table of type size \(r\) has at most \(m^r\) entries. Since products of disjoint types combine coefficients entrywise, these tables can be computed in

\[
m^{2d/3}\operatorname{poly}(s,d)
\]

arithmetic operations. This is smaller than \(m^{52d/75}\), because

\[
\frac23<\frac{52}{75}.
\]

The pairwise inner products contribute at most

\[
s^2m^{(52/75+\varepsilon)d+o(d)}
\]

operations. Therefore, subject to the exact rational implementation in Section 7, the full set-multilinear PIT procedure has the conditional running-time bound

\[
\boxed{
T_{\rm PIT}
=m^{(52/75+\varepsilon)d+O(1)}
\operatorname{poly}(s,d,L,\log m).}
\]

Its correctness conditions remain those of the original integer PIT theorem:

- if the output polynomial is nonzero, the algorithm rejects;
- if the output polynomial is zero and every gate satisfies the stated coefficient \(\ell_1\)-norm bound, the algorithm accepts;
- if the output polynomial is zero but an intermediate gate violates that bound, either answer may occur.

The original paper states the weaker exponent \(d-\lceil d/6\rceil\) for its full procedure. The above improvement uses the faster contraction for the inner-product stage and the sharper direct enumeration bound \(m^{2d/3}\) for the other coefficient-table stages.

## 7. Exact rational arithmetic and bit complexity

The rectangular exponent theorem is an arithmetic-operation statement. To obtain a bit-time bound over integer inputs, an exact rational implementation is required.

The PIT theorem is conditional on the correctness of the rectangular exponent preprint and on converting its characteristic-zero exponent bound into a finite rational scheme with the height control below. A sufficient construction is as follows. Fix \(\varepsilon>0\). By the characteristic-zero rectangular exponent bound, choose a finite rational bilinear scheme for one fixed base size \(N_0\) that multiplies

\[
N_0\times N_0^2\quad\text{by}\quad N_0^2\times N_0
\]

using at most \(N_0^{25/8+\varepsilon}\) bilinear products. The base scheme is fixed once \(\varepsilon\) is fixed. Let \(D\) be a common denominator of its rational coefficients, and let \(C\) bound the relevant coefficient \(\ell_1\)-sums.

Recursing this base scheme \(\ell\) levels gives matrices whose dimension is proportional to \(N_0^\ell\). The common denominator and coefficient height grow at most as

\[
D^{O(\ell)}\quad\text{and}\quad C^{O(\ell)}.
\]

Since \(\ell=O(\log N)\), these quantities have \(O_\varepsilon(\log N)\) bits. For input entries of at most \(B\) bits, the intermediate exact rational values therefore have bit length

\[
O_\varepsilon(B+\log N).
\]

The final matrix product is exactly the ordinary integer matrix product when its inputs are integer matrices, so its output entries are integers even though some intermediate values may be rational. Exact numerator/denominator arithmetic consequently incurs only a polynomial bit-cost overhead per arithmetic operation.

In the PIT application, the source algorithm bounds its integer intermediates by a quantity of bit length

\[
B=O(sL+d\log(2m)+\log s).
\]

Here \(N\) is at most a fixed power of \(m^d\), so \(\log N=O(d\log m)\). The rational matrix products therefore preserve a polynomial bit-time overhead, yielding the stated conditional PIT running time.

**What remains to verify:** the argument above should be expanded into a standalone lemma giving the exact coefficient-height recurrence for the chosen finite base scheme. The rectangular preprint supplies the asymptotic exponent, while the finite rational base scheme and its recursive height bound are the bridge to a deterministic Turing-machine time bound. The constants may be very large and depend on \(\varepsilon\); this is an existence result, not a practical algorithm specification.

## 8. What this says about SAT and P versus NP

The assignment-polynomial encoding has the form

\[
P_F^{(d)}=\sum_{\mu:F(\mu)=1}\prod_{j=1}^d x_{j,\mu|_{V_j}},
\]

so, over the integers,

\[
F\in\mathrm{SAT}\quad\Longleftrightarrow\quad P_F^{(d)}\not\equiv0.
\]

This encoding does not itself make the polynomial small: it can have up to \(m^d\) monomials. The cited complexity paper uses a universal partition polynomial and a PIT framework to obtain a Boolean–arithmetic win–win theorem. Replacing its PIT subroutine by the conditional faster subroutine above would improve a quantitative running-time parameter in that proof, but would not change the theorem's logical alternatives.

In particular, this work does **not** establish \(P=NP\), \(P\ne NP\), a polynomial-time SAT algorithm, or an unrestricted tensor-contraction lower bound. The representation problem for the universal partition polynomial remains separate and unresolved by the present argument.

## 9. Limitations and next verification steps

Before submission as a research article, the following work is still needed:

1. **Independent verification of the rectangular exponent source.** The \(25/8\) input is from a recent preprint. The present note relies on that result and does not reprove its tensor-spectrum argument.
2. **A complete rational-scheme height lemma.** State the selected finite base scheme, derive the coefficient and denominator recurrences, and connect rational arithmetic cost to Turing bit complexity.
3. **A full PIT proof with all stages counted.** The \(m^{2d/3}\) preprocessing bound and the modified pairwise contraction should be integrated into one proof, including the \(\varepsilon\)-loss and all polynomial factors.
4. **Formal verification beyond the optimization lemma.** The Lean file supplied with this note checks the real-variable four-case inequality and the tight example. It does not formalize matrix multiplication, the heavy decomposition, the coefficient-height argument, or the PIT theorem.
5. **A literature review.** The exact fraction and optimization statement need to be compared with prior work before claiming priority.

## References

1. Przemysław Uznański, *Rectangular matrix multiplication from polynomial products*, [arXiv:2610.10494v2](https://arxiv.org/abs/2610.10494), 11 October 2026. The paper states \(\omega(1,k,1)\leq 1+k+1/(4k)\) for \(k\geq1/2\), and states that the exponent bounds hold over characteristic-zero fields.
2. Nikolai Chukhin, Karthik Gajulapalli, Alexander Golovnev, and Ivan Mihajlin, *A Little Derandomization Goes a Long Way: Unconditional Circuit Lower Bounds using Low-Degree PIT*, [arXiv:2611.07972](https://arxiv.org/abs/2611.07972), 5 November 2026. See its set-multilinear integer PIT theorem and the heavy-decomposition/inner-product construction.
3. Amir Shpilka, *Exposition of OpenAI's Matrix Multiplication in Exponent 9/4 (and an explicit algorithm)*, [ECCC Report TR26-281](https://eccc.weizmann.ac.il/report/2026/281/), 27 October 2026. This square-matrix result is not needed for the \(52/75\) derivation presented here.

---

## Appendix A. Formalization scope

The accompanying `Cycle6.lean` file formalizes the central inequality

\[
\max\left(v+\frac78\min(u,V/2),\ u+\frac78\min(v,U/2)\right)\geq\frac{23d}{75}
\]

under the decomposition and feasibility assumptions, together with the tight configuration. This is the mathematically self-contained part of the argument. The external rectangular matrix-multiplication theorem and the end-to-end PIT construction are not assumed as Lean axioms in that file.
