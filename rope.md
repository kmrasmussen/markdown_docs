# ROUND AND ROUND WE GO! WHAT MAKES ROTARY POSITIONAL ENCODINGS USEFUL
Federico Barbero
https://arxiv.org/pdf/2410.06205

# RoPE
Attention logits (pre-softmax) are computed

NoPE: No positional embeddings: $a_{ij} = q_i^Tk_j$
RoPE: Rotational position embeddings: $a_{ij} = q_i R^{j-i} k_j$

$R^{j-i}$ is orthogonal block-wise diagonal matrix.

You divide up the k_j in pieces of 2 dimensions each. Each block in in the matrix rotates 2-d vector by g_k^(j-i), where $g_k = \theta^{-2(d-1)/d}$, where $\theta$ is the base frequency and is usually ~10K, but experiments with 500K.

$Rope(q_i, k_j) = (R_i q_i)^T (R_j k_j) = q_i^T R_i^T R_j k_j = q_i R^{j-i} k_j$

# Paper ideas
- Low frequencies and high frequencies are used for different things. First frequencies are the g_k, and R^{j-i} has block matrices
for rotation matrices based on $g_k^{j-i}$, so here $j-i$ is a bit equivalent to the time variable. When you have high frequencies, you spin it around so fast that the resulting rotated keys will be so sensitive to $j-i$, and so the entire rope attention activation is very sensitive to position. This is not the case for low frequencies, the rotated keys are generally closer. This could mean more of the "semantics" of the keys are maintained for low frequencies.
- The paper investigates Gemma7b empirically with the conclusion that high frequencies are used for constructing attention matrices that are using relative position rather than semantic similarity. They find attention matrices that are diagonal - these matrices at least intuitively do not really have any use-case, they will just result in the head outputs corresponding to the value vectors at the same position. But this is not really a residual connection right? Even a linear transformation by W_V could still be valuable in the larger scheme of things, and when you add LayerNorm on top, even more so. They also find heads that have attention matrices with attention to the previous token. Again, this is an example of attention matrices that are not based on semantics. 