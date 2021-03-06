Requirements
============

|Codename| works with Python3

You will also need:

-  `numpy <http://www.numpy.org>`_ and `SciPy <http://www.scipy.org>`_

-  `emcee <https://emcee.readthedocs.io/en/stable/>`_ and/or `dynesty <https://dynesty.readthedocs.io/en/latest/>`_ for inference (Please cite these packages in any publications)

-  `sedpy <https://github.com/bd-j/sedpy>`_ (for filter projections)

- `HDF5 <https://www.hdfgroup.org/HDF5/>`_ and `h5py <http://www.h5py.org>`_
  (If you have Enthought or Anaconda one or both of these may already be installed,
  or you can get HDF5 from homebrew or macports)

For modeling galaxies you will need:

-  `FSPS <https://github.com/cconroy20/fsps>`_ and
   `python-FSPS <https://github.com/dfm/python-FSPS>`_ (Please cite these packages in any publications)

You probably also need to have `AstroPy <https://astropy.readthedocs.org/en/stable/>`_
for FITS file processing and cosmological calculations, please cite this package in any publications.

For parallel processing with emcee you will need:

-  MPI (e.g. openMPI or mvapich2, available from homebrew, macports, or Anaconda)  and
   `mpi4py <http://pythonhosted.org/mpi4py/>`_

Installation
============

|Codename| itself is is pure python.  However, several other packages are required (see above.)
To install |Codename| and its dependencies to a conda environment, use the following procedure:

.. code-block:: shell

        # change this if you want to install elsewhere;
        # or, copy and run this script in the desired location
        CODEDIR=$PWD

        # Create and activate environment (named 'prospector')
        cd $CODEDIR
        git clone git@github.com:bd-j/prospector.git
        cd prospector
        conda env create -f environment.yml
        conda activate prospector
        cd ..

        # Install FSPS from source
        git clone git@github.com:cconroy20/fsps
        export SPS_HOME="$PWD/fsps"
        cd $SPS_HOME/src
        make clean; make all

        # Install other repos from source
        repos=( dfm/python-fsps bd-j/sedpy )
        for r in "${repos[@]}"; do
            git clone git@github.com:$r
            cd ${r##*/}
            python setup.py install
            cd ..
        done

        cd prospector
        python setup.py install

        echo "Add 'export SPS_HOME=$SPS_HOME' to your .bashrc"


To install just |Codename|

.. code-block:: shell

		cd <install_dir>
		git clone https://github.com/bd-j/prospector
		cd prospector
		python setup.py install

Then in Python

.. code-block:: python

		import prospect

.. |Codename| replace:: Prospector
