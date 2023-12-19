# Information Theory Revision

## Probability Theory

**Keywords:** Trial, (elementary) outcome, sample space, events, conditional probabilities, Bayes formula, marginal distribution.

**Notations:**  

- $|A|$: Number of possible occurrences of event A.
- $P(A)$: Probability of A occurring.
- $p(x)=p(X=x)$
- $p_{X|Y}(x|y)$

**Normal Distribution:**

$$p(x) = \frac{1}{\sqrt{2\pi}\sigma}e^{\frac{(x-\mu)^2}{2\sigma^2}}$$

## Entropy

### Random variable

**Keywords:** alphabet, probability mass vector, expected value.

## Shannon Content Information (SIC)
Given a random variable X, the SIC of X having the value of x is:
$$SIC=-log_{2}{(p(x))}$$

## Entropy
### Formula
Measures the uncertainty of a random variable
$$H(X)=E(-\log_{2}{p(x)})$$
### Joint Entropy
$$H(X, Y)=E(-\log_{2}{p_{X,Y}(x, y)})$$

### Conditional Entropy
Conditional Entropy measures the amount of additional information in Y knowing X
$$H(X|Y)=E(-\log_{2}{p_{X|Y}(x|y)})$$

### Chain Rule
Refers to the Venn diagram

### Relative Entropy
Measures the difference between 2 distributions of the same random variable
$$D(p||q)=E(p(x)\log_{2}{\frac{p(x)}{q(x)}})$$

### Mutual Information
Measures the reduction in the uncertainty of X knowing Y and vice versa.
$$I(X, Y)=E(\log_2{\frac{p(x, y)}{p(x)p(y)}})$$

## Inequalities
**Keywords:** Concex, concave
### Jensen's Inequality
$$E(f(X)) \ge f(E(X))$$

### Information Inequalities
$$H(X) \le log|H(X)| $$
$$D(p||q) \ge 0$$
$$I(X, Y) \ge 0$$
and other rules extracted from the Venn diagram

### Fano Inequality
States that the error of inferring X from Y has a minimum probability of:
$$p_e \ge \frac{H(X|Y) - H(p_e)}{\log{|X|}}$$
If this inferrence Z conforms $Z \subset X$, strict form can be applied:
$$p_e \ge \frac{H(X|Y) - H(p_e)}{\log{(|X| - 1)}}$$

## Asymptotic Equipartition
**Asymtotic:** Extremely close but not there.
### Law of Large Numbers  

- Measuring the average height of everyone on Earth is infeasible.
- Taking average of smaller groups is.
- Define $S_n$ as the average of a random variable X in a sample of size n.
- The average of these averages is:
  $$E(S_n)=E(X)$$
- But variance is different:
  $$var(S_n)=\frac{var(X)}{n}$$

### Typical Set

- A sample $S_n$ of a random variable X is typical if, given $H(X)$:
  $$\sum{-\log{p(X)} = nH(X)}$$
  with p(X) derived from the distribution of X, not $S_n$
- Average:
  $$E(-\log{p(X_{seq})})=nH(X)$$
- The typical set of samples is defined as (for predefined $H(X)$ and $\epsilon$):
  $$A_{\epsilon}(n)=\{X \in X^n : |-n^{-1}\log{p(X_{seq})} - H(X)| < \epsilon\}$$
- Propterties:
  - Sequence probability: $2^{-n(\epsilon + H(X))} < p(X_{seq}) < 2^{-n(-\epsilon + H(X))}$
  - Total Propability: $p(X_{seq} \in A_{\epsilon}(n)) > 1 - \epsilon$ with $n > N_{\epsilon}$
  - Typical set's size: $(1-\epsilon)2^{n(H(X)-\epsilon)} < |A_{\epsilon}(n)| \le 2^{n(H(X) + \epsilon)}$

## Data Compression (or Source Coding)
### Goal
Encode data into fewer bits
### Expected Length
$$L(C)=\sum_{x\in X}p(x)l(x)$$
### Nonsingular Code
A code is nonsingular if every element of the range of X maps into a different string:
$$x1 \ne x2 \rightarrow C(x1) \ne C(x2)$$

### Extension Of A Code
$$C(x_1, x_2, ..., x_n) = C(x_1)C(x_2)...C(x_n)$$

### Uniquely Decodable Codes
 A code is called uniquely decodable if its extension is nonsingular. In other words,
any encoded string in a uniquely decodable code has only one possible source string producing it. However, one may have to look at the entire string to determine even the first symbol in the corresponding source string.

### Prefix Code
A code is called a prefix code or an instantaneous code if no codeword is a prefix of any other codeword.

### Kraft Inequality
For any prefix code over an alphabet of size D:
$$\sum{D^{-l_i}} \le 1$$

## Source Coding Algorithms

### Optimal Code
For a D-ary code, the minimum expected codelength sastifies:
$$H_D(X) \le L(C) \le H_D(X) + 1$$

Higher probability => shorter codeword length.

### Huffman Coding
Easy but remember to pad dummy symbols to reach $1 + k(D - 1)$ in case of D-ary coding

### Shannon Coding
#### Idea
Calculate cumulative probability, then convert to binary and use some inital bits as codeword:
$$F(X) = \sum_{a \le x}p(a) + p(x) / 2$$
Precision taken: $l(x)=[-\log_2{p(x)}] + 1$

#### Variation
1. Put the probs in decreasing order.
2. Split as close to 50-50 as possible.
3. Repeat with each half.
### Universal Coding
#### Problem Statement
Shannon and Huffman coding require predefined distribution. Therefore, they are not optimal for streaming.

#### Properties
- Independent of source's distribution.
- Compress sequences rather than symbols.
- Example:
  $$WWWBBWWWWBBBWW \rightarrow 3W2B4W3B2W$$

### Lempel-Ziv LZ78
Easy