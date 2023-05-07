Ansible Role: Downloader
========================

An Ansible role that downloads and extracts an executable out of an archive. Used for installing binaries.

Requirements
------------

N/A

Role Variables
--------------

| Variable                             |   Type   |     Default      | Description                                                                                   |
| :----------------------------------- | :------: | :--------------: | :-------------------------------------------------------------------------------------------- |
| `downloader_download_url`            | `string` |      `N/A`       | The url to download.                                                                          |
| `downloader_download_dest`           | `string` |      `/tmp`      | The path at which to download the given url.                                                  |
| `downloader_download_validate_certs` |  `bool`  |      `true`      | Whether or not to validate the certificates for the download url.                             |
| `downloader_unarchive`               |  `bool`  |     `false`      | Whether or not the downloaded file is an archive which needs to be expanded.                  |
| `downloader_unarchive_dest`          | `string` |      `/tmp`      | The path at which to expand the archive. Required if `downloader_unarchive` is set to `true`. |
| `downloader_executable_src`          | `string` |      `N/A`       | The path to the executable file which needs to be installed.                                  |
| `downloader_executable_dest`         | `string` | `/usr/local/bin` | The path at which to move the executable file.                                                |
| `downloader_executable_mode`         | `string` |      `0755`      | The permissions of the executable file.                                                       |

Dependencies
------------

N/A

Example Playbook
----------------

Installing the terraform package via the prebuilt binaries:

``` yaml
- name: Install terraform
  hosts: localhost
  beome: true
  gather_facts: true

  tasks:
    - name: Install unzip
      ansible.builtin.apt:
        name: unzip
        state: present
        update_cache: true

    - name: Include role
      ansible.builtin.include_role:
        name: mirceanton.downloader
      vars:
        downloader_download_url: https://releases.hashicorp.com/terraform/1.3.3/terraform_1.3.3_linux_amd64.zip
        downloader_download_dest: /tmp/terraform_1.3.3_linux_amd64.zip
        downloader_unarchive: true
        downloader_unarchive_dest: /tmp
        downloader_executable_src: /tmp/terraform
        downloader_executable_dest: /usr/bin/terraform
        downloader_executable_mode: 0755
```

License
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
