# COMPUTE CANADA

The lab applies for storage space and compute time on Compute Canada every year.
These resources are limited and are to be shared fairly across members of the lab.
Given that no member of the lab has priviledged admin rights, this fairness relies on everyone adopting a clear code of conduct, and shared organization.
If not, other members of the lab will see their analysis/data transfer/... fail, and they will be discouraged to use these incredible resources, and to do research at all.

When you are new to Compute Canada, we will ask you to run a setup script that will set data management access and give you access to utils for project management, including:

- setup ACLs for the data admin to the project and nearline folders
- add project management commands to your bash environment
- generate SSH keys if not already created, and help you set them up on Github for easier access
- configure the ssh agent and keychain to avoid typing your ssh key password each time you push to github or ssh to another server.
- configure git global variables


You can do it just once on each cluster:

```
/project/def-pbellec/share/data_admin/utils/setup_user_account.sh
```

When you download a dataset:

1. Contact the lab's data admins, Basile and Arnaud, prior to downloading the data, and ask how to best proceed if uncertain.
1. Please use BIDS storage if available, and use datalad to "install" the dataset
2. Data should be store in `~/project/(rrg|def)-pbellec/DATA`
4. Create a folder for the dataset in  `~/project/(rrg|def)-pbellec/DATA/new_dataset/derivatives`
3. To set the access rights there are two possible cases:

  5.1. For datasets that requires the applicants to sign individual non-sharing agreement.

  When applying, it is important that you involve the lab's data admins so they can also sign the non-sharing agreement or other nescessary documents.

  Set read access rights through ACLs to all your colleagues who have signed the agreement, and will be using the data. Be sure to also give read access rights to the lab's data admins.

  ```
  setfacl -R -m u:colleague1:rX u:colleague2:rX .... u:admin1:rX u:admin2:rX ... ~/projects/rrg-pbellec/DATA/new_dataset
  ```

  If the other colleagues will contribute to the analysis, give them write access to the derivatives folders.

  ```
  setfacl -R -m u:colleague1:rwX u:colleague2:rwX ~/projects/rrg-pbellec/DATA/new_dataset/derivatives
  ```

 5.2 For all other types of datasets.

For datasets that do not require individuals to sign non-sharing agreeements you can give read access to anyone. This means fellow lab members who are interested in using the same dataset can do so without re-dowloading/duplicating/wasting storage.

  ```
  chmod -R g+r ~/projects/rrg-pbellec/DATA/new_dataset
  ```
  And give write access to the derivatives
  ```
  chmod -R g+rw ~/projects/rrg-pbellec/DATA/new_dataset/derivatives
  ```

 4. When you run preprocessing, analysis, .... store the outputs in the derivatives folder, with an explicit naming, and a version of the software used, eg.

```
~/projects/rrg-pbellec/DATA/new_dataset/derivatives/fmriprep-20.0.4
~/projects/rrg-pbellec/DATA/new_dataset/derivatives/my_fancy_new_analysis-0.0.2
```
  Same as above, you must, at a minimim, give read access to the data admins.

When you install a new software, yours, or others, install it in the `SRC` folder.
