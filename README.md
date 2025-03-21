# `condaenvlist`

[![License GPL v3](https://img.shields.io/badge/license-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0.en.html) [![Python 3.6+](https://img.shields.io/badge/python-3.6%2B-blue.svg)](https://www.python.org/downloads/)


Like many bioinformaticians, I rely on [conda](https://www.anaconda.com/docs/getting-started/miniconda/main) to install software, organise tools into functional groups and avoid (at least somewhat) problems with conflicting dependencies. But I often find myself confused by my own conda environments. Which tools are in which environments? When did I last update an environment? Are the tools in an environment up to date?

So I created `condaenvlist` as a replacement for `conda env list`. It shows the information I actually need: a description of each environment, the date it was last updated and the versions of key tools. To provide the description and specify which tools are key, the user adds a simple `envinfo.txt` file to each environment directory.



## Example output

<pre><code><b>base</b>
  Description:  Python with some common packages (NumPy, Pandas, etc) for general use.
  Location:     /Users/wickr/miniconda3
  Last updated: 21 Mar 2025
  Key tools:
   • python 3.12.9

<b>autocycler</b>
  Description:  Autocycler and long-read assemblers. Autocycler's executable and scripts are
                linked to my development directory, so they are always up-to-date.
  Location:     /Users/wickr/miniconda3/envs/autocycler
  Last updated: 20 Mar 2025
  Key tools:
   • autocycler (version unknown)
   • canu 2.3
   • flye 2.9.5
   • metamdbg 1.1
   • miniasm 0.3
   • minipolish 0.1.3
   • necat 0.0.1_update20200803
   • raven-assembler 1.8.3

<b>polishing</b>
  Description:  My favourite polishers for bacterial genomes, mainly for use on Autocycler
                assemblies. Also contains my compare_assemblies.py script for comparing pre-
                polish and post-polish assemblies.
  Location:     /Users/wickr/miniconda3/envs/polishing
  Last updated: 21 Mar 2025
  Key tools:
   • medaka 2.0.1
   • polypolish 0.6.0
   • pypolca 0.3.1</code></pre>



## Example `envinfo.txt` file

Contents of `/Users/wickr/miniconda3/envs/polishing/envinfo.txt`:
```
My favourite polishers for bacterial genomes, mainly for use on Autocycler assemblies. Also contains my compare_assemblies.py script for comparing pre-polish and post-polish assemblies.
medaka, polypolish, pypolca
```

The first line is the environment description and is required.

The second line is a comma-delimited list of key software tools. It determines which tools are shown in the output. This list is optional – if omitted, no key tools will be shown by `condaenvlist`.

`condaenvlist` uses `conda list` to determine tool versions. This works for most packages installed via `conda` or `pip`, but not for tools installed manually (e.g. binaries copied into the environment's `bin` directory, as with `autocycler` in the example above).



## Requirements

`condaenvlist` requires [Python](https://www.python.org/) 3.6 or later. It’s a standalone script with no external dependencies (only the standard library).



## Installation

`condaenvlist` is a single script. Just copy it to a directory in your `PATH`:
```bash
git clone https://github.com/rrwick/condaenvlist
cp condaenvlist/condaenvlist ~/.local/bin
```

To get the most out of `condaenvlist`, create an `envinfo.txt` file in each of your conda environments (see example above).



## License

[GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.html)
