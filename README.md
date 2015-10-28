cyvlfeat
========

[![Join the chat at https://gitter.im/menpo/cyvlfeat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/menpo/cyvlfeat?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
A Python (cython) wrapper of the VLFeat library

We intend for this to be a light wrapper around the [VLFeat](http://www.vlfeat.org/) toolbox. cyvlfeat will provide a mixture of pure Python and Cython code that looks to replicate the existing Matlab toolbox. Cython is intended to fulfill the role of ``mex`` files.

We respect the original BSD 2-clause license and thus release this wrapper under the same license.

We thank the authors of VLFeat for their contribution to the computer vision community.

Current State
-------------
At the moment, only the basics of the SIFT package is implemented. This includes implementations of the SIFT and Dense SIFT functions. These two methods replicate the ``vl_sift`` and ``vl_dsift`` methods. None of the other helper methods are implemented, but should be fairly simply to replicate in pure Python using Matplotlib.

To install cyvlfeat, we **strongly suggest you use conda**:

    conda install -c menpo cyvlfeat
  
If you don't want to use conda, your mileage will vary. In particular, you must satisfy the linking/compilation requirements for the package, which include the ``vlfeat`` dynamic library.

Development
-----------
To develop cyvlfeat (to extend its functionality), you will need to be comfortable using Cython. To begin re-implementing Matlab's ``mex`` methods in Cython, you will to install the following requirements:

  - cython >=0.22
  - numpy >= 1.9
  - vlfeat >= 0.9.20

To make this easier, we suggest you use [conda](http://conda.pydata.org/miniconda.html). This makes installing the dependencies much simpler.

This library **dynamically** links against the ``vlfeat``, and therefore you will need to ensure that it is available to the Python setup environment at build time. As mentioned, this is mostly easily done using conda:

    conda config --add channels menpo
    conda install cyvlfeat
    conda remove cyvlfeat

This will install all of cyvlfeat's dependencies, including ``vlfeat``, ``numpy`` and ``cython``. You will likely want to install this into a new conda environment for cyvlfeat development. Please see the [conda documentation](http://conda.pydata.org/docs/faq.html#managing-environments) for an explanation about environments. 

To begin developing, you will need to git fork and clone this repository:

  - Fork using the Github fork button
  - Clone your repo:  ``git clone git@github.com:YOUR_GITHUB_USERNAME/cyvlfeat.git``
  - Add this repo as **upstream**:  ``git remote add upstream git@github.com:menpo/cyvlfeat.git``

You can now locally install a development version/build cyvlfeat by using:

    CFLAGS="-I/PATH_TO_MINICONDA/miniconda/envs/CONDA_ENV_NAME/include" LDFLAGS="-I/PATH_TO_MINICONDA/miniconda/envs/CONDA_ENV_NAME/lib" pip install -e ./

This will build and install a local version of cyvlfeat for your development. You can also build and test this by using conda itself (from inside the cyvlfeat git repository):

    conda install conda-build
    conda build ./conda

Which simulate building the conda package, including running tests. To run the tests manually, ensure ``nose`` is installed, and run

    nosetests -v .

From inside the git repository.

To add a new feature, please start a pull request. This will also kick off the automated building systems for both Linux and Windows. I will oversee any new additions, and providing they pass on both automated build systems, will merge the new functionality in.
