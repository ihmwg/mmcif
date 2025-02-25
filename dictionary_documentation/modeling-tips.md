## Integrative modeling tips

It is helpful to keep in mind from the very beginning of an integrative
modeling study that it will eventually be deposited as mmCIF in
[PDB-IHM](https://pdb-ihm.org/), as it is often difficult to gather
all of the pertinent information after the fact (e.g. at publication time).
Below are some tips based on the experience of researchers using the
[IMP](https://integrativemodeling.org/) software in
[Andrej Sali's lab](https://salilab.org).

### Tracking of modeling inputs and protocols

The mmCIF file format does not only capture the coordinates of the final
models, but can also describe the input data used, the modeling protocol,
and even point to intermediate or additional models (e.g. modeling
trajectories in binary format, or all conformations in an ensemble, only a
subset of which are deposited directly as mmCIF). To store this information,
track changes to it as a function of time, and work effectively with
experimental and computational collaborators, it is recommended to use a
repository hosted publicly with a system such as [GitHub](https://github.com)
or [GitLab](https://gitlab.com).
This also allows for the modeling to be reproduced, which while not a
strict requirement for deposition in PDB-IHM, is increasingly demanded
by journals. (The repository should also be given one or more README files
to describe how to reproduce the modeling.) For example, the Sali lab's
modeling of the Nup84 subcomplex of the yeast nuclear pore complex (NPC) is
[available at GitHub](https://github.com/integrativemodeling/nup84)

In order for data to be stored permanently, it needs to be assigned a
[Digital Object Identifier (DOI)](https://www.doi.org/). A number of free
services exist to archive data with a DOI, such as [Zenodo](https://zenodo.org)
and [Figshare](https://figshare.com). It is straightforward to upload a
snapshot of a GitHub repository to these services, and also add
modeling outputs (which are typically too large to place in a GitHub
repository). For example, the Nup84 modeling from above is available at
[10.5281/zenodo.1218053](https://doi.org/10.5281/zenodo.1218053).

### Experimental data should be deposited

Any experimental data used in the modeling (such as electron microscopy (EM)
maps, crosslinks, small angle X-ray data, etc.) needs to be available.
Ideally it should be deposited in the appropriate database. For example
any EM maps should be placed in [EMDB](http://www.emdatabank.org/). These
depositions can take time to process, so should be done well before publication,
if possible. Where accession codes aren't available (e.g. if a suitable
database does not exist) a DOI can be used instead.

### Raw, not processed data

Most integrative modeling software works with input data that has been
processed in some fashion. For example, a modeling run may take as
input a PDB file that itself was generated by comparative modeling or docking.
For maximum utility, all models deposited in PDB-IHM should link back to
the raw, not processed, data that was used (for example, to allow future
modeling to improve on these models by reprocessing the input data). Thus,
the modeling repository should include instructions or appropriate control
files to reproduce this preprocessing. For example, comparative models
generated by [MODELLER](https://salilab.org/modeller/) can be reproduced by
including the Modeller Python script and PIR alignment used. Similarly,
processed experimental data should be linked back to raw data where
appropriate (for example, EM maps can link back to the EM micrographs, and
crosslinks can link back to the mass spectrometry peaklists).

### Automate generation of mmCIF files

While it is certainly possible to generate mmCIF files by hand, or in a
semi-automatic fashion (e.g. by converting a traditional PDB file to mmCIF
and then handling IHM-specific fields manually) it is generally easier
to use a software library to handle this. One such package is
[python-ihm](https://github.com/ihmwg/python-ihm). This be used directly by
writing a Python script to gather modeling inputs, protocols, and outputs -
for an example, see the Sali lab's modeling of the
[Nup133 component of the yeast NPC](https://github.com/integrativemodeling/nup133/tree/master/outputs_foxs_ensemble_new/pdb-dev). Alternatively, it can be
interfaced with other modeling packages. For example,
[IMP](https://integrativemodeling.org/) provides a
[ProtocolOutput class](https://integrativemodeling.org/nightly/doc/ref/classIMP_1_1pmi_1_1mmcif_1_1ProtocolOutput.html) which will
generate mmCIF files automatically as a side effect of the normal modeling -
this class was used by the [Nup84 modeling](https://github.com/integrativemodeling/nup84/blob/master/scripts/nup84.isd.modeling.withXrayInterface.py)
referenced above.
