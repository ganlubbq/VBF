******
CLEFIA
******

Description
===========

*CLEFIA* is a proprietary block cipher algorithm, developed by Sony. It is intended to be used in DRM systems. It is among the cryptographic techniques recommended candidate for Japanese government use by CRYPTREC revision in 2013. It has two :math:`8 \times 8` S-boxes: :math:`S_0,S_1`

Summary
=======

+-------+------+-----+-------+------+---------+----------------+--------------+-----------+
| S-box | *NL* |*LD* | *DEG* | *AI* | *MAXAC* | :math:`\sigma` | *LP*         | *DP*      |
+=======+======+=====+=======+======+=========+================+==============+===========+
| S0    | 100  | 40  | 6     | 4    | 96      | 269056         | 0.0478515625 | 0.0390625 |
+-------+------+-----+-------+------+---------+----------------+--------------+-----------+
| S1    | 112  | 56  | 7     | 4    | 32      | 133120         | 0.015625     | 0.015625  |
+-------+------+-----+-------+------+---------+----------------+--------------+-----------+

S0
==

Representations
---------------

Polynomial function over :math:`\gf{GF(2^8)}` with irreducible polynomial :math:`x^8 + x^4 + x^3 + x^2 + 1`: `Trace representation <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0-trace.pdf>`_

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.wal>`_

Walsh Spectrum representation (except first row and column):

.. image:: /images/Clefia0.png
   :width: 750 px
   :align: center

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S0.ac>`_

Other useful information in cryptanalysis
-----------------------------------------

Cycle structure:

+--------------+------------------+
| Cycle length | Number of cycles |
+==============+==================+
| 4            | 1                |
+--------------+------------------+
| 5            | 2                |
+--------------+------------------+
| 17           | 1                |
+--------------+------------------+
| 109          | 1                |
+--------------+------------------+
| 116          | 1                |
+--------------+------------------+

There are no linear structures

It has no fixed points. 

It has 2 negated fixed points: (0,1,0,0,0,0,0,1), (1,1,1,1,1,1,0,1)

Construction
------------

:math:`S_0` is generated by combining four 4-bit S-boxes :math:`SS_0,SS_1,SS_2` and :math:`SS_3` in the following way:

Step 1. :math:`\vec{t_0}=SS_0(\vec{x_0}), \ \vec{t_1}=SS_1(\vec{x_1})` where :math:`\vec{x} = \vec{x_0} | \vec{x_1}, \vec{x_i} \in \gf{V_4}`

Step 2. :math:`\vec{u_0}=\vec{t_0}+0x2 \cdot \vec{t_1}, \ \vec{u_1}= 0x2 \cdot \vec{t_0}+\vec{t_1}`

Step 3. :math:`\vec{y_0}=SS_2(\vec{u_0}), \ \vec{y_1}=SS_3(\vec{u_1})` where :math:`\vec{y} = \vec{y_0} | \vec{y_1}, \vec{y_i} \in \gf{V_4}`

Tables of CLEFIA S-boxes :math:`SS_i (0 \leq i \leq 3)`:

+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| x      | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | a | b | c | d | e | f |
+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| SS0(x) | e | 6 | c | a | 8 | 7 | 2 | f | b | 1 | 4 | 0 | 5 | 9 | d | 3 |
+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| SS1(x) | 6 | 4 | 0 | d | 2 | b | a | 3 | 9 | c | e | f | 8 | 7 | 5 | 1 |
+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| SS2(x) | b | 8 | 5 | e | a | 6 | 4 | c | f | 7 | 2 | 3 | 1 | 0 | d | 9 |
+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| SS3(x) | a | 2 | 6 | d | 3 | 4 | 5 | e | 0 | 7 | 8 | 9 | b | f | c | 1 |
+--------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

The multiplication in :math:`0x2 \cdot \vec{t_i}` is performed in :math:`\gf{GF(2^4)}` defined by the lexicographically first primitive polynomial :math:`x^4+x+1`. Here we provide the table of multiplication of :math:`0x2` with an element modulo :math:`x^4+x+1`. The entries in the Table are represented in hexadecimal notation for compactness. The column indices represent the element to be multplied by :math:`0x2` modulo :math:`x^4+x+1`, and the product is the corresponding entry in the column. 

Table of the multiplication :math:`0x2 \cdot \vec{x}`:

+---------------------------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| :math:`\vec{x}`           | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | a | b | c | d | e | f |
+---------------------------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| :math:`0x2 \cdot \vec{x}` | 0 | 2 | 4 | 6 | 8 | a | c | e | 3 | 1 | 7 | 5 | b | 9 | f | d |
+---------------------------+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

Next figure shows the construction of :math:`S_0`:

.. image:: /images/ClefiaS0Construction.png
   :width: 750 px
   :align: center

Hence, CLEFIA S0 can be denoted by:

:math:`S_0(\vec{x_0},\vec{x_1}) = \left( SS_2 \left( SS_0(\vec{x_0}) \oplus Mul2 \left( SS_1(\vec{x_1}) \right) \right), SS_3 \left( Mul2 \left( SS_0(\vec{x_0}) \right) \oplus SS_1(\vec{x_1}) \right) \right)`

Note that the symbol :math:`\circ` refers to the composition of functions, :math:`\oplus` refers to the direct sum of functions and :math:`Mul2(\vec{x}) = 0x2 \cdot \vec{x}`.

The criteria of several constructions in :math:`S_0` are summarized in the following tables:

.. image:: /images/ClefiaS0NL.png
   :width: 750 px
   :align: center

.. image:: /images/ClefiaS0deg.png
   :width: 750 px
   :align: center

You can find a program which calculates the Truth Tables of these constructions in chapter "Operations and constructions over Vector Boolean Functions", section "Addition of coordinate functions".

Mul2
^^^^

Let :math:`Mul2(\vec{x}) = 0x2 \cdot \vec{x}` the multiplication in :math:`\gf{GF(2^4)}` defined by the primitive polynomial :math:`x^4+x+1` as in CLEFIA cipher.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.ac>`_

Cycle structure:

+--------------+------------------+
| Cycle length | Number of cycles |
+==============+==================+
| 1            | 1                |
+--------------+------------------+
| 15           | 1                |
+--------------+------------------+

There are 225 linear structures

`Linear Structures <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/Mul2.ls>`_

It has 1 fixed point: (0,0,0,0) 

It has 1 negated fixed point: (0,1,0,1)

:math:`0x2 \cdot \vec{t_1}`
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The operation :math:`0x2 \cdot \vec{t_1}` in Step 2 can be interpreted as the composition of :math:`Mul2` and :math:`SS_1`.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t1.ac>`_

Cycle structure:

+--------------+------------------+
| Cycle length | Number of cycles |
+==============+==================+
| 1            | 2                |
+--------------+------------------+
| 2            | 2                |
+--------------+------------------+
| 10           | 1                |
+--------------+------------------+

There are 3 linear structures:

.. code-block:: console

   ([0 0 1 0],[0 1 0 1])
   ([0 1 0 0],[0 1 0 1])
   ([0 1 1 0],[0 1 0 1])

It has 2 fixed points: (0,1,0,0), (0,1,0,1)

It has 1 negated fixed point: (1,1,0,0)

:math:`0x2 \cdot \vec{t_0}`
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The operation :math:`0x2 \cdot \vec{t_0}` in Step 2 can be interpreted as the composition of :math:`Mul2` and :math:`SS_0`.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/0x2t0.ac>`_

Cycle structure:

+--------------+------------------+
| Cycle length | Number of cycles |
+==============+==================+
| 16           | 1                |
+--------------+------------------+

There are 3 linear structures:

.. code-block:: console

   ([0 0 1 1],[1 0 0 1])
   ([1 0 0 1],[1 0 0 1])
   ([1 0 1 0],[1 0 0 1])

It has no fixed points.

It has 1 negated fixed point: (0,0,0,0)

:math:`\vec{u_0}`
^^^^^^^^^^^^^^^^^

The operation :math:`\vec{u_0} = \vec{t_0} \oplus 0x2 \cdot \vec{t_1}` in Step 2 can be interpreted as the direct sum of :math:`SS_0` and :math:`Mul2 \circ SS_1`.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u0.ac>`_

There are 6 linear structures:

.. code-block:: console

   ([0 0 0 0 0 0 1 0],[0 1 0 1])
   ([0 0 0 0 0 1 0 0],[0 1 0 1])
   ([0 0 0 0 0 1 1 0],[0 1 0 1])
   ([0 0 1 1 0 0 0 0],[1 1 0 0])
   ([1 0 0 1 0 0 0 0],[1 1 0 0])
   ([1 0 1 0 0 0 0 0],[1 1 0 0])

:math:`\vec{u_1}`
^^^^^^^^^^^^^^^^^

The operation :math:`\vec{u_1}= 0x2 \cdot \vec{t_0} \oplus \vec{t_1}` in Step 2 can be interpreted as the direct sum of :math:`Mul2 \circ SS_0` and :math:`SS_1`.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/u1.ac>`_

There are 6 linear structures:

.. code-block:: console

   ([0 0 0 0 0 0 1 0],[1 0 1 0])
   ([0 0 0 0 0 1 0 0],[1 0 1 0])
   ([0 0 0 0 0 1 1 0],[1 0 1 0])
   ([0 0 1 1 0 0 0 0],[1 0 0 1])
   ([1 0 0 1 0 0 0 0],[1 0 0 1])
   ([1 0 1 0 0 0 0 0],[1 0 0 1])

:math:`\vec{y_0}`
^^^^^^^^^^^^^^^^^

In the Step 3, :math:`\vec{y_0}` is obtained by composing :math:`SS_2` S-box with :math:`\vec{u_0}`.

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y0.ac>`_

There are no linear structures.

:math:`\vec{y_1}`
^^^^^^^^^^^^^^^^^

In the Step 3, :math:`\vec{y_1}` is obtained by composing :math:`SS_3` S-box with :math:`\vec{u_1}`. 

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.wal>`_

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/y1.ac>`_

There are no linear structures.

S1
==

Representations
---------------

Polynomial function over :math:`\gf{GF(2^8)}` with irreducible polynomial :math:`x^8 + x^4 + x^3 + x^2 + 1`: `Trace representation <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1-trace.pdf>`_

`Polynomial representation in ANF <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.pdf>`_

`Truth Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.tt>`_

`ANF Table <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.anf>`_

`Characteristic function <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.char>`_

`Walsh Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.wal>`_

Walsh Spectrum representation (except first row and column):

.. image:: /images/Clefia1.png
   :width: 750 px
   :align: center

`Linear Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.lp>`_

`Differential Profile <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.dp>`_

`Autocorrelation Spectrum <https://raw.githubusercontent.com/jacubero/VBF/master/Clefia/S1.ac>`_

Other useful information in cryptanalysis
-----------------------------------------

Cycle structure:

+--------------+------------------+
| Cycle length | Number of cycles |
+==============+==================+
| 256          | 1                |
+--------------+------------------+

There are no linear structures

It has no fixed points. 

It has 1 negated fixed point: (0,0,1,1,1,0,1,0)

