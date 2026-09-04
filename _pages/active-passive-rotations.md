---
permalink: /notes/active-passive-rotations/
title: "Active and Passive Rotations"
author_profile: true
---

When learning transformations as an undegraduate student, I remember being confused if a given rotation $$R$$ is meant to rotate a point (e.g., by rotating the coordinate vector representing the point) or rotate the coordinate frame that the point is represented in.
For example, imagine a clock where you can rotate the clock separately from the hands of the clock:

<div style="margin-left: 2em;">

<p>(i) You can think of rotating a point (i.e., coordinate vector) as rotating one of the hands on the clock without moving the base of the clock (e.g., if the hand is at 12:00, a +90 degree rotation of the hand will place the hand on 9:00).</p>

<p>(ii) You can think of rotating the coordinate frame as rotating the base of the clock without moving the hands of the clock (e.g., if the hand is at 12:00, a +90 degree rotation of the base of the clock will place the hand on 3:00).</p>

</div>

The main point is that these two interpretations correspond to inverse rotations: rotating a point by an angle $$\theta$$ is equivalent to leaving the point fixed and rotating the coordinate frame by $$-\theta$$.

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

**Proof.** Consider the active rotation of a point $$\mathbf{p}$$ to onto new point $$\mathbf{p}'$$ (i.e., moving the hands of the clock without moving the base of the clock) given by

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

Thus, $$\mathtt{B} = \mathtt{A}^{-1}$$ since $$\mathbf{p} = \mathtt{B}\mathbf{p}' = \mathtt{A}^{-1}\mathbf{p}'$$ from the active rotation above. A similar derivation for a change of basis can be found in an answer on Mathematics Stack Exchange.[^2] $$\blacksquare$$

The main point is that the transformation between frame A and frame B can be visualized by rotating frame $$A$$ until aligned with frame $$B$$.
However, such a transformation is active not passive, and the difference is important.
The rotation matrix that rotates a point from frame A to frame B (i.e., $${}^B\mathtt{R}_A$$) is not the same as rotating frame A onto frame B (i.e., $${}^A\mathtt{R}_B$$).

[^1]: [https://en.wikipedia.org/wiki/Active_and_passive_transformation](https://en.wikipedia.org/wiki/Active_and_passive_transformation)
[^2]: [Rotating a point vs. rotating coordinate system, Mathematics Stack Exchange](https://math.stackexchange.com/questions/1110681/rotating-a-point-vs-rotating-coordinate-system)