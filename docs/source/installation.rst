Installation
============

1. Obtain Python 3.5 and virturalenv.

2. Create a virtual environment somewhere on your disk, and then activate it.

  ::

  $ virtualenv --no-site-packages --python=python3.5 micti_env
  $ source micti_env/bin/activate


3. Download the source code and install the requirements.

  ::

  $ pip install MICTI

  pip will install the following packages:

  * `NumPy <http://www.numpy.org/>`_
  * `SciPy <http://www.scipy.org/>`_
  * `matplotlib <http://matplotlib.org/>`_
  * `pandas <http://matplotlib.org/>`_
  * `gprofiler <https://biit.cs.ut.ee/gprofiler/>`_
  * `seaborn <https://seaborn.pydata.org/>`_
  * `scikit-learn <https://scikit-learn.org/>`_
 
4. Import MICTI.

   ::

   $from MICTI import MARKER
