<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>

# Transformácie

## Translácia
$$ 
T(a,b,c) =
\begin{bmatrix} 
1 & 0 & 0 & a \\
0 & 1 & 0 & b \\
0 & 0 & 1 & c \\
0 & 0 & 0 & 1
\end{bmatrix}
 $$

## Škálovanie

$$ 
S(a,b,c) =
\begin{bmatrix} 
a & 0 & 0 & 0 \\
0 & b & 0 & 0 \\
0 & 0 & c & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
 $$

## Rotácia
$$ 
R_z(a,b,c) =
\begin{bmatrix} 
cos(a) & -sin(a) & 0 & 0 \\
sin(a) & cos(a) & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
 $$

$$ 
R_y(a,b,c) =
\begin{bmatrix} 
cos(a) & 0 & sin(a) & 0 \\
0 & 1 & 0 & 0 \\
-sin(a) & 0 & cos(a) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
 $$

$$ 
R_x(a,b,c) =
\begin{bmatrix} 
1 & 0 & 0 & 0 \\
0 & cos(a) & -sin(a) & 0 \\
0 & sin(a) & cos(a) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
 $$
 
## Skladanie transformácií
Ak skladáme transformácie, ktoré dopredu nepoznáme,

$$
X^n = \mathbf{A}_n \cdot (\ldots(\mathbf{A}_2 \cdot (\mathbf{A}_1 \cdot X + \vec{d}_1) + \vec{d}_2)\ldots) + \vec{d}_n
$$