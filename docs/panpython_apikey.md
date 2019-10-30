---
id: panpython_apikey
title: API Key Generation
sidebar_label: API Key Generation
---

> The **panxapi.py** **-k** option performs the `type=keygen` API request
to generate the API key for an administrator account. The **-h** and
**-l** (ell) options specify the hostname or IP address of the firewall
and username and password arguments for the API request.

## Generate API Key

    panxapi.py -h 10.30.11.101 -l admin:admin -k

> Example output:

    keygen: success
    API key:  "LUFRPT14MW5xOEo1R09KVlBZNnpnemh0VHRBOWl6TGM9bXcwM3JHUGVhRlNiY0dCR0srNERUQT09"

> For brevity, the labs use the superuser administrator account `admin`;
creating API administrator accounts using a custom admin role with the
least privilege set of XML API types required for your usage, is
recommended.

> A [.panrc](https://github.com/kevinsteves/pan-python/blob/master/doc/panrc.rst)
file contains hostname and API key variables optionally referenced by a
*tagname* using the **panxapi.py** **-t** option. The `.panrc` file is a convenient way to store
API keys for all your firewalls in a file, then reference those keys by
tag when executing API calls. You'll create a .panrc file in `Lab 2` at
the bottom of this page and use it for all following API calls.

> When **-t** is combined with **-h**, **-l** and **-k**, **panxapi.py**
writes `.panrc` format lines with the `hostname` and `api_key` variables
to *stdout*.

## Generate `.panrc` without *tagname*

> Use a null string for the *tagname* to create tagless variables; these
are matched when **-t** is not specified.

    panxapi.py -t '' -h 10.30.11.101 -l admin:admin -k

> Example output:

    keygen: success
    # panxapi.py generated: 2017/04/08 09:05:42
    hostname=10.30.11.101
    api_key=LUFRPT14MW5xOEo1R09KVlBZNnpnemh0VHRBOWl6TGM9bXcwM3JHUGVhRlNiY0dCR0srNERUQT09

## Generate `.panrc` with *tagname*

    panxapi.py -t xapilab -h 10.30.11.101 -l admin -k

> Example output: 

    Password:
    keygen: success
    # panxapi.py generated: 2017/04/08 09:08:47
    hostname%xapilab=10.30.11.101
    api_key%xapilab=LUFRPT14MW5xOEo1R09KVlBZNnpnemh0VHRBOWl6TGM9bXcwM3JHUGVhRlNiY0dCR0srNERUQT09

> When the password is not specified on the command line the user is
prompted for it. This is useful to avoid leaving the password in the
shell history.

## Create `.panrc` file using shell output redirection

> Shell output redirection can be used to create your `.panrc` file.

    panxapi.py -t xapilab -h 10.30.11.101 -l admin -k >> ~/.panrc

> Example output:

    Password:
    keygen: success

> Set least privilege permissions:
    
    chmod 600 ~/.panrc

> The `.panrc` file contains authentication material; it should have
strict file permissions (read/write for the owner, and not accessible by
group or other).

> The `.panrc` file entries with your *tagname* are verified by performing
an operational command API request with **-o** *cmd*.