---
permalink: /notes/active-passive-rotations/
title: "Active and Passive Rotations"
author_profile: true
---

**Passive Rotation.** We can talk about rotations in the context of representing points, vectors, and objects in different coordinate frames.
The transformation between these coordinate frames are called *passive transformations*.
In other words, if we are given the coordinates of a point $$\mathbf{p}$$ in reference frame $$A$$ denoted $${}^A \mathbf{p}$$, we can compute the coordinates of that point in reference frame $$B$$ denoted $${}^B \mathbf{p}$$.
Here, we are essentially changing the point of view of the point $$p$$ from view $$A$$ to view $$B$$, and the change of view is expressed as $${}^B \mathbf{p} = {}^B \mathtt{R}_A {}^A \mathbf{p}$$.

**Active Rotation.** Now, suppose we want to rotate a point $$\mathbf{p}$$ by some angle $$\theta$$ to obtain a point $$\mathbf{p}'$$.
In other words, instead of changing our point of view, we rotate the point (represented as a coordinate vector) changing the physical position.
This is called an *active transformation* and is realized by rotating our coordinate axis by $$-\theta$$.

<img src="/images/notes/active_versus_passive.jpg" alt="Active and passive rotations" style="display: block; margin-left: auto; margin-right: auto; width: 60%;">

*Figure 1: (Left) Example of active rotation changing physical position of P. (Right) Example of passive rotation changing the point of view of point P. Notice P′ in the left image has coordinates identical to P in the right image after applying the passive rotation.*[^1]

In general, an active rotation $$\mathtt{A}$$ of a coordinate vector is realized by a rotation $$\mathtt{A}^{-1}$$ of the coordinate axes (referred to as a passive rotation).

**Proof.** Consider the active rotation of a point $$\mathbf{p}$$ to a new point $$\mathbf{p}'$$ given by

$$
\mathbf{p'} = \mathtt{A}\mathbf{p}
$$

where $$\mathtt{A}$$ is a rotation matrix.
Now, instead of physically changing the position of $$\mathbf{p}$$, we want to write $$\mathbf{p}'$$ by changing the point of view.
In this context, the vector is unchanged, and the coordinate system is rotated.
To do this, we apply a change of basis where the original base vectors $$\mathbf{e}_i$$ are rotated onto the new base vectors $$\mathbf{e}'_i$$ given by

$$
\mathbf{e}'_i = \mathtt{B} \mathbf{e}_i
$$

where $$i \in \{1,\cdots,n\}$$ and $$\mathtt{B}$$ is a rotation matrix. Thus, we can write

$$
\mathbf{p} = \sum_{i=1}^n p_i \mathbf{e}_i = \sum_{i=1}^n p_i' \mathbf{e}'_i = \sum_{i=1}^n p_i' \mathtt{B} \mathbf{e}_i = \sum_{i=1}^n \mathtt{B} p_i' \mathbf{e}_i = \mathtt{B} \sum_{i=1}^n p_i' \mathbf{e}_i = \mathtt{B} \mathbf{p}'.
$$

Thus, $$\mathtt{B} = \mathtt{A}^{-1}$$ since $$\mathbf{p} = \mathtt{B}\mathbf{p}' = \mathtt{A}^{-1}\mathbf{p}'$$ from the active rotation above. $$\blacksquare$$

We can think of active transformations as mechanism for visualizing passive transformations.
For example, the transformation between frame A and frame B can be visualized by rotating frame $$A$$ until aligned with frame $$B$$.
However, such a transformation is active not passive, and the difference is important.
The rotation matrix that rotates a point from frame A to frame B (i.e., $${}^B\mathtt{R}_A$$) is not the same as rotating frame A onto frame B (i.e., $${}^A\mathtt{R}_B$$).
This also applies to transformations that include both rotation and translation components.

[^1]: [https://en.wikipedia.org/wiki/Active_and_passive_transformation](https://en.wikipedia.org/wiki/Active_and_passive_transformation)