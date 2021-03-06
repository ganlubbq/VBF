*******
Summary
*******

+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| Operations and constructions over VBF                                                     			         				              |
+================================================+====================================================================================================================+
| **SYNTAX**                                     | **DESCRIPTION**                          									      |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`long operator==(VBF& F, VBF& G)`        | Returns *1* if *F* and *G* are equal     								              |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void Comp(VBF& X, VBF& F, VBF& G)`      | :math:`X = G \circ F`                    								              |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void inv(VBF& X, VBF& A)`               | :math:`X = F^{-1}`                       								              |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void sum(VBF& X, VBF& F, VBF& G)`       | :math:`X = F+G`                          									      |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void directsum(VBF& X, VBF& F, VBF& G)` | :math:`X = F \oplus G`                   								              |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void concat(VBF& X, VBF& F, VBF& G)`    | :math:`X(\vec{x},x_{n+1}) =\left( x_{n+1}+1 \right) F(\vec{x})+ x_{n+1} G(\vec{x})`                                |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void concatpol(VBF& X, VBF& F, VBF& G)` | :math:`X(x_1,\ldots,x_{n_1},x_{n_1+1},\ldots,x_{n_1+n_2}) = F(x_1,\ldots,x_{n_1})+G(x_{n_1+1},\ldots,x_{n_1+n_2})` |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void addimage(VBF& X, VBF& F, VBF& F)`  | :math:`X = (F,G)`                        									      |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| :code:`void bricklayer(VBF& X, VBF& F, VBF& G)`| :math:`X = F | G`                        									      |
+------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+

