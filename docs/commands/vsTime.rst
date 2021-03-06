vsTime
======

**Parameter as a function of time**

This can be used to extract the parameter of either a specific base-pair/step
or over a DNA segment as a function of time.

**Usage:**

.. code-block:: bash

    usage: dnaMD vsTime [-h] [-i L-BP_cdna.dat] [-o output.dat]
                    [-tbp total-bp-number] [-p parameter]
                    [-bs bp/s-start-number] [-be bp/s-end-number]
                    [-mm sum-or-mean] [-fbp 1]


**Optional arguments:**

.. code-block:: bash

    -h, --help            show this help message and exit
    -i L-BP_cdna.dat, --input L-BP_cdna.dat
                        Name of input file (from do_x3dna or hdf5 file).
                        This file should contain the required parameters. It can be a file either
                        produced from do_x3dna or hdf5 storage file.

    -o output.dat, --output output.dat
                        Name of output file.
                        The extracted output will be written in output file.

    -tbp total-bp-number, --total-bp total-bp-number
                        Total number of basepair in DNA/RNA.
                        It is an essential input.

    -p parameter, --parameter parameter
                        Parameter name.
                        This parameter will be extracted from file. Ensure that parameter is present
                        in the file, otherwise wrong values will be extracted from file.

    -bs bp/s-start-number, --bp-start bp/s-start-number
                        First BP/BPS of DNA after which parameter will be extracted.
                        If it is not given, first basepair or base-step will be considered.

    -be bp/s-end-number, --bp-end bp/s-end-number
                        Last BP/BPS of DNA upto which parameter will be extracted.

                        If it is not given, parameter for only a single bp/s given with -bs/--bp-start
                        option will be extracted.

    -mm sum-or-mean, --merge-method sum-or-mean
                        Method to merge the parameter of a DNA segment from local parameters
                        of all base-pairs/steps that are within the range given by '-bs' and '-be'.

                        Currently accepted keywords are as follows:
                            * mean : Average of local parameters
                            * sum : Sum of local parameters

                        When only "-bs" option is provided without "-be", then -mm/--merge-method is
                        not required.

    -fbp 1, --first-bp 1  Basepair number of first base-pair.
                        Usually it is one. Therefore, if this option is not provided, base-pair
                        numbering will start from one.

                        In rare cases, base-pair numbering might start with other number. In those
                        cases, use this option to start numbering of basepair from other number than
                        one.


Example
-------

.. code-block:: bash

    dnaMD vsTime -i fdna.h5 -tbp 60 -bs 10 -be 50 -p "curvature" -mm sum -o curv.dat

Following output is obtained in ``curv.dat`` file.

::

    # Time 	 "curvature"
    0.0	0.14487306619300122
    100.0	0.24987540226819524
    200.0	0.19187540226819527
    300.0	0.20787540226819526
    400.0	0.26187540226819517
    500.0	0.24582073103934177
    600.0	0.23887540226819526
    700.0	0.2478754022681953
    800.0	0.2558754022681952
    .
    .
    .

It can be plotted by xmgrace as following:

.. code-block:: bash

    xmgrace curv.dat


The obtained plot is similar to the curvature plot
`shown here <../notebooks/helical_axis_tutorial.html#To-calculate-curvature-and-tangent-vectors-along-helical-axis>`_
for 10-50 bp length.
