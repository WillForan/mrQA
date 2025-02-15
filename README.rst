==============================
Quickstart
==============================

.. image:: https://img.shields.io/pypi/v/mrQA.svg
        :target: https://pypi.python.org/pypi/mrQA

.. image:: https://img.shields.io/travis/Open-Minds-Lab/mrQA.svg
        :target: https://travis-ci.com/Open-Minds-Lab/mrQA

.. image:: https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg
        :target: https://nbviewer.org/github/Open-Minds-Lab/mrQA/blob/master/examples/usage.ipynb

mrQA suite of tools
-------------------
 - automatic evaluation of protocol compliance
 - Documentation: https://open-minds-lab.github.io/mrQA/
 - Tutorial: https://nbviewer.org/github/Open-Minds-Lab/mrQA/blob/master/examples/usage.ipynb

CLI usage
---------
A protocol compliance report can be generated directly from the command line
interface. For a DICOM dataset::

    mr_proto_compl --data_root /path/to/dataset --style xnat

For a BIDS dataset::

    mr_proto_compl --data_root /path/to/dataset --style bids

Python usage
------------
To use  mrQA in a project::

    import  mrQA

The most important methods for checking protocol compliance is
``check_compliance``. It calls all the required functions.

* To infer the most frequent values for each acquisition parameter
* Aggregate the non-compliance information to generate an HTML report


First of all, you have to import the relevant modules and classes::

    from MRdataset import import_dataset
    from mrQA import check_compliance

Given a dataset of MR images, (e.g. DICOM images), we create
``MRdataset.base.Project`` object. This can be achieved simply by
``MRdataset.import_dataset`` method, which requires a valid folder path.
For details on ``MRdataset``, please see its documentation. ::

    data_root = '/home/user/datasets/ABCD'
    output_dir = '/home/user/MR_reports/'
    dataset = import_dataset(data_root=data_root,
                             style='xnat',
                             name='ABCD')

    check_compliance(dataset=dataset, output_dir=output_dir)

And that's it! Please note some important points:

* It will generate a corresponding HTML file in the ``output_dir`` which contains the complete report.
* ``style`` denotes the specific format of neuroimaging dataset. For example, use *xnat* for DICOM datasets and *bids* for BIDS datasets
* ``name`` is an identifier which can be used to reload the the cached files later.If no name is specified, it uses a random identifier.

