## OpenSimplex 2 - SuperSimplex & Fast Simplex-Style Gradient Noise

Successors to OpenSimplex Noise, plus updated OpenSimplex. Includes 2D and 3D noise. 4D noise is coming!

* The provided 3D function in **SuperSimplexNoise** ("OpenSimplex 2, smooth version") is about as fast as optimized OpenSimplex, but has better uniformity.

* The provided 3D function in **FastSimplexStyleNoise** ("OpenSimplex 2, faster version") is about as fast as common Simplex noise implementations, but uses a much different process.

* The 2D functions aren't intended to represent new developments in the same vein as the 3D functions. They are just the logical pairings. Both 2D functions are implemented using lookup tables, and perform similar to or faster than the average.

* All functions are given new gradient sets that are symmetric with the lattice, but don't cause neighboring vertex gradients to constructively interfere.

The classes in [java/areagen](https://github.com/KdotJPG/New-Simplex-Style-Gradient-Noise/tree/master/java/areagen) offer speed-optimized whole-area generators, which operate by flood-fill queue on the noise lattice. (i.e. they don't use a "range")

* The only differences between the two versions's area generators are: **radius parameter** and **normalization constant**.
  * The radius can be straightforwardly reduced for faster noise, or increased for smoother noise. There are no geometric traversal steps to cause discontinuities, and no hardcoded point computations to limit performance increases, as would be the case with varying the radius in the evaluators.
  * The normalization constant is baked into the same gradient set as the evaluator. It can be recomputed using [Noise Normalizer](https://github.com/KdotJPG/NoiseNormalizer). If left as is, the noise will still function correctly, it will just have a different output range.

#### TODO:

* 4D noise
* More language ports
* Consolidate render tiles in readme into fewer images
* Move radius into unified constant
* Test 24-gon instead of 12-gon for 2D gradient set, and replace if results nicer.

#### Maybe TODO:

* Create combined FastSimplexStyleNoise and SuperSimplexNoise in one file, reducing repetition for someone who needs both.
* Include octave summation, ridged noise, etc.
* Exponentially-distributed noise ([source of idea](http://jcgt.org/published/0004/02/01/))
* Simultaneous multi-instance evaluation
* Disc/Ball-output noise (Outputs 2D/3D/etc. vector for more directionally-uniform domain warping)
* Tileable 2D noise (slightly mis-skewed triangular grid which repeats properly over a desired rectangle)
* Tileable 3D noise (using an extension of the above)
* Tileable 3D noise (exact, using the "classic" lattice orientation)

#### Change Log
* Slightly reorganized description above, and added TODO/changelog. (Jan 23, 2020)
* Renamed / additionally named the noise "OpenSimplex (2.0)", separated into two versions/variants. (Jan 23, 2020)
  * SuperSimplex and FastSimplexStyleNoise are very similar to each other algorithmically, and are in the same spirit as the original OpenSimplex.
  * OpenSimplex is used in a lot of projects, and the naming might help facilitate adoption of the new noise in its place.
* Add C# ports of evaluators. (Jan 13, 2020)
* Create separate files which include area generators. (Jan 13, 2020)
* Renamed PlaneFirst evaluators to XYBeforeZ, and added XZBeforeY. (Jan 13, 2020)
* Fixed equals() method in AreaGenLatticePoint3D for area generators. (Dec 24, 2019)

## Renders

### SuperSimplexNoise, 2D

![SuperSimplexNoise, 2D](images/ssn2.png?raw=true)

### FastSimplexStyleNoise, 2D

![FastSimplexStyleNoise, 2D](images/fssn2.png?raw=true)

### Updated OpenSimplexNoise, 2D

![SuperSimplexNoise, 3D (Classic, 2D slice)](images/osn2.png?raw=true)

---

### SuperSimplexNoise, 3D (Classic, 2D slice)

![Updated OpenSimplexNoise, 2D](images/ssn3c.png?raw=true)

### FastSimplexStyleNoise, 3D (Classic, 2D slice)

![FastSimplexStyleNoise, 3D (Classic, 2D slice)](images/fssn3c.png?raw=true)

### Updated OpenSimplexNoise, 3D (Classic, 2D slice)

![Updated OpenSimplexNoise, 3D (Classic, 2D slice)](images/osn3c.png?raw=true)

---

### SuperSimplexNoise, 3D (PlaneFirst, 2D slice)

![SuperSimplexNoise, 3D (PlaneFirst, 2D slice)](images/ssn3pf.png?raw=true)

### FastSimplexStyleNoise, 3D (PlaneFirst, 2D slice)

![FastSimplexStyleNoise, 3D (PlaneFirst, 2D slice)](images/fssn3pf.png?raw=true)

### Updated OpenSimplexNoise, 3D (PlaneFirst, 2D slices)

![Updated OpenSimplexNoise, 3D (PlaneFirst, 2D slice at z=0.0)](images/osn3pfa.png?raw=true)

![Updated OpenSimplexNoise, 3D (PlaneFirst, 2D slice at z=0.5)](images/osn3pfb.png?raw=true)

---

### Updated OpenSimplexNoise, 4D (2D slice)

![Updated OpenSimplexNoise, 4D (PlaneFirst, 2D slice)](images/osn4.png?raw=true)


## Performance Metrics

### SuperSimplex vs OpenSimplex (2D)

![2D Metrics SuperSimplexNoise](images/metrics_ssn2.png?raw=true)

It would appear that the older 2D OpenSimplex comes out ahead of the refactored version. But DigitalShadow's 3D and especially 4D refactorings come out ahead. The results may have been different had I tested in the original C# language of the refactored version, rather than Java.

### FastSimplexStyleNoise vs others (2D)

![2D Metrics FastSimplexStyleNoise](images/metrics_fssn2.png?raw=true)

### SuperSimplex vs OpenSimplex (3D)

![3D Metrics SuperSimplexNoise](images/metrics_ssn3.png?raw=true)

### FastSimplexStyleNoise vs others (3D)

![3D Metrics FastSimplexStyleNoise](images/metrics_fssn3.png?raw=true)

### OpenSimplex legacy vs DigitalShadow's refactor (4D)

![4D Metrics OpenSimplexNoise](images/metrics_osn4.png?raw=true)


## Public Domain Dedication

This is free and unencumbered software released into the public domain. See UNLICENSE. To the best of my non-lawyer knowledge, no patent claims cover anything implemented here (not legal advice). Please use this software to make cool things, rather than to make patents! Enjoy.
