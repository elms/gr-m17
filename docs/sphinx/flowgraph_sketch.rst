Flowgraph
=========

.. graphviz::

   digraph D{
     node [shape=record];
     {rank=same c0 c1 golay_24_12}
     {rank=same p0 p1}
     {rank=same i0 i1}

     c0[label="conv coder"]
     p0[label="Puncture P1"]
     i0[label="interleave"]
     s0[label="add sync"]
     chunker_48[label="chunk 48 bits"]
     golay_24_12[label="golay(24, 12)"]

     c1[label="conv coder"]
     p1[label="Puncture P2"]
     i1[label="interleave"]
     s1[label="add sync"]
     fn[label="Add FN"]
     chunker_128[label="chunk 128 bits"]

     framecomb[label="Frame Combiner"]
     supercomb[label="Superframe Combiner"]

     LICH -> c0 -> p0 -> i0 -> s0 -> supercomb
     LICH -> chunker_48 -> golay_24_12 -> framecomb
     data -> chunker_128 -> fn -> CRC -> c1 -> p1 -> framecomb
     framecomb -> i1 -> s1 -> supercomb
     Preamble -> supercomb
   }
