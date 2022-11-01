Ansible Role: Downloader
========================

An Ansible role that downloads and extracts an executable out of an archive. Used for installing binaries.

Requirements
------------

N/A

Role Variables
--------------

|         Variable          |     Type     |              Default              |                           Description                            |
| :-----------------------: | :----------: | :-------------------------------: | :--------------------------------------------------------------: |
|    `downloader_prereq`    | list(string) | `[unzip, gzip, bzip2, xzip, tar]` |              List of archiving utilities required.               |
| `downloader_archive_url`  |    string    |            `UNDEFINED`            |            Path or URL where the archive is located.             |
| `downloader_archive_dest` |    string    |            `UNDEFINED`            | Path to where the archive should be downloaded and extracted to. |
|   `downloader_exec_src`   |    string    |            `UNDEFINED`            |         Path at which to find the downloaded executable.         |
|  `downloader_exec_dest`   |    string    |            `UNDEFINED`            |         Path at which to copy the downloaded executable.         |
|  `downloader_exec_mode`   |    string    |              `0755`               |            Permissions for the downloaded executable.            |

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

  roles:
    - name: mirceanton.downloader
      vars:
        downloader_archive_url: https://releases.hashicorp.com/terraform/1.3.3/terraform_1.3.3_linux_amd64.zip
        downloader_archive_dest: /tmp
        downloader_exec_src: /tmp/terraform
        downloader_exec_dest: /usr/bin/terraform
```

License
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
