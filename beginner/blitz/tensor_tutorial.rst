.. note::
    :class: sphx-glr-download-link-note

    Click :ref:`here <sphx_glr_download_beginner_blitz_tensor_tutorial.py>` to download the full example code
.. rst-class:: sphx-glr-example-title

.. _sphx_glr_beginner_blitz_tensor_tutorial.py:


What is PyTorch?
================

It’s a Python based scientific computing package targeted at two sets of
audiences:

-  A replacement for NumPy to use the power of GPUs
-  a deep learning research platform that provides maximum flexibility
   and speed

Getting Started
---------------

Tensors
^^^^^^^

Tensors are similar to NumPy’s ndarrays, with the addition being that
Tensors can also be used on a GPU to accelerate computing.



.. code-block:: python


    from __future__ import print_function
    import torch







Construct a 5x3 matrix, uninitialized:



.. code-block:: python


    x = torch.empty(5, 3)
    print(x)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[ 1.7514e+13,  4.5643e-41, -8.9364e-04],
            [ 3.0684e-41,  4.4842e-44,  0.0000e+00],
            [ 6.7262e-44,  0.0000e+00, -8.9364e-04],
            [ 3.0684e-41,  0.0000e+00,  1.4013e-45],
            [-2.9063e-05,  3.0684e-41, -8.8470e-04]])


Construct a randomly initialized matrix:



.. code-block:: python


    x = torch.rand(5, 3)
    print(x)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[0.7051, 0.3457, 0.5862],
            [0.1563, 0.5782, 0.2913],
            [0.5500, 0.4929, 0.0750],
            [0.2212, 0.5570, 0.0271],
            [0.8127, 0.4764, 0.6952]])


Construct a matrix filled zeros and of dtype long:



.. code-block:: python


    x = torch.zeros(5, 3, dtype=torch.long)
    print(x)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[0, 0, 0],
            [0, 0, 0],
            [0, 0, 0],
            [0, 0, 0],
            [0, 0, 0]])


Construct a tensor directly from data:



.. code-block:: python


    x = torch.tensor([5.5, 3])
    print(x)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([5.5000, 3.0000])


or create a tensor based on an existing tensor. These methods
will reuse properties of the input tensor, e.g. dtype, unless
new values are provided by user



.. code-block:: python


    x = x.new_ones(5, 3, dtype=torch.double)      # new_* methods take in sizes
    print(x)

    x = torch.randn_like(x, dtype=torch.float)    # override dtype!
    print(x)                                      # result has the same size





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[1., 1., 1.],
            [1., 1., 1.],
            [1., 1., 1.],
            [1., 1., 1.],
            [1., 1., 1.]], dtype=torch.float64)
    tensor([[-0.5493, -0.5388,  0.0475],
            [ 1.0198,  1.3793,  0.1465],
            [ 0.0544, -0.3469, -0.5106],
            [-1.0559, -0.6729,  0.5385],
            [ 0.1552, -0.7012,  0.0211]])


Get its size:



.. code-block:: python


    print(x.size())





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    torch.Size([5, 3])


.. note::
    ``torch.Size`` is in fact a tuple, so it supports all tuple operations.

Operations
^^^^^^^^^^
There are multiple syntaxes for operations. In the following
example, we will take a look at the addition operation.

Addition: syntax 1



.. code-block:: python

    y = torch.rand(5, 3)
    print(x + y)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[ 0.2939, -0.1781,  0.3123],
            [ 1.0412,  1.7882,  0.9534],
            [ 0.3938,  0.0133, -0.4562],
            [-1.0467, -0.6081,  0.6843],
            [ 0.8699, -0.2994,  0.7823]])


Addition: syntax 2



.. code-block:: python


    print(torch.add(x, y))





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[ 0.2939, -0.1781,  0.3123],
            [ 1.0412,  1.7882,  0.9534],
            [ 0.3938,  0.0133, -0.4562],
            [-1.0467, -0.6081,  0.6843],
            [ 0.8699, -0.2994,  0.7823]])


Addition: providing an output tensor as argument



.. code-block:: python

    result = torch.empty(5, 3)
    torch.add(x, y, out=result)
    print(result)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[ 0.2939, -0.1781,  0.3123],
            [ 1.0412,  1.7882,  0.9534],
            [ 0.3938,  0.0133, -0.4562],
            [-1.0467, -0.6081,  0.6843],
            [ 0.8699, -0.2994,  0.7823]])


Addition: in-place



.. code-block:: python


    # adds x to y
    y.add_(x)
    print(y)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([[ 0.2939, -0.1781,  0.3123],
            [ 1.0412,  1.7882,  0.9534],
            [ 0.3938,  0.0133, -0.4562],
            [-1.0467, -0.6081,  0.6843],
            [ 0.8699, -0.2994,  0.7823]])


.. note::
    Any operation that mutates a tensor in-place is post-fixed with an ``_``.
    For example: ``x.copy_(y)``, ``x.t_()``, will change ``x``.

You can use standard NumPy-like indexing with all bells and whistles!



.. code-block:: python


    print(x[:, 1])





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([-0.5388,  1.3793, -0.3469, -0.6729, -0.7012])


Resizing: If you want to resize/reshape tensor, you can use ``torch.view``:



.. code-block:: python

    x = torch.randn(4, 4)
    y = x.view(16)
    z = x.view(-1, 8)  # the size -1 is inferred from other dimensions
    print(x.size(), y.size(), z.size())





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    torch.Size([4, 4]) torch.Size([16]) torch.Size([2, 8])


If you have a one element tensor, use ``.item()`` to get the value as a
Python number



.. code-block:: python

    x = torch.randn(1)
    print(x)
    print(x.item())





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([0.1171])
    0.11707398295402527


**Read later:**


  100+ Tensor operations, including transposing, indexing, slicing,
  mathematical operations, linear algebra, random numbers, etc.,
  are described
  `here <http://pytorch.org/docs/torch>`_.

NumPy Bridge
------------

Converting a Torch Tensor to a NumPy array and vice versa is a breeze.

The Torch Tensor and NumPy array will share their underlying memory
locations, and changing one will change the other.

Converting a Torch Tensor to a NumPy Array
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^



.. code-block:: python


    a = torch.ones(5)
    print(a)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([1., 1., 1., 1., 1.])



.. code-block:: python


    b = a.numpy()
    print(b)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    [1. 1. 1. 1. 1.]


See how the numpy array changed in value.



.. code-block:: python


    a.add_(1)
    print(a)
    print(b)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    tensor([2., 2., 2., 2., 2.])
    [2. 2. 2. 2. 2.]


Converting NumPy Array to Torch Tensor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
See how changing the np array changed the Torch Tensor automatically



.. code-block:: python


    import numpy as np
    a = np.ones(5)
    b = torch.from_numpy(a)
    np.add(a, 1, out=a)
    print(a)
    print(b)





.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    [2. 2. 2. 2. 2.]
    tensor([2., 2., 2., 2., 2.], dtype=torch.float64)


All the Tensors on the CPU except a CharTensor support converting to
NumPy and back.

CUDA Tensors
------------

Tensors can be moved onto any device using the ``.to`` method.



.. code-block:: python


    # let us run this cell only if CUDA is available
    # We will use ``torch.device`` objects to move tensors in and out of GPU
    if torch.cuda.is_available():
        device = torch.device("cuda")          # a CUDA device object
        y = torch.ones_like(x, device=device)  # directly create a tensor on GPU
        x = x.to(device)                       # or just use strings ``.to("cuda")``
        z = x + y
        print(z)
        print(z.to("cpu", torch.double))       # ``.to`` can also change dtype together!






**Total running time of the script:** ( 0 minutes  0.008 seconds)


.. _sphx_glr_download_beginner_blitz_tensor_tutorial.py:


.. only :: html

 .. container:: sphx-glr-footer
    :class: sphx-glr-footer-example



  .. container:: sphx-glr-download

     :download:`Download Python source code: tensor_tutorial.py <tensor_tutorial.py>`



  .. container:: sphx-glr-download

     :download:`Download Jupyter notebook: tensor_tutorial.ipynb <tensor_tutorial.ipynb>`


.. only:: html

 .. rst-class:: sphx-glr-signature

    `Gallery generated by Sphinx-Gallery <https://sphinx-gallery.readthedocs.io>`_
