# To install and use a virtual environment

## Why use a VE?

A virtual environment (VE, or sometimes venv) is a tool that helps to keep dependencies required by different projects separate by creating isolated Python virtual environments for them. You can have different VEs for different versions of tools (eg, for one tool that requires Python 3.9 vs another that requires Python 3.11). VEs let you have stable, reproducible, and portable environments. You are in control of which packages versions are installed and when they are upgraded. It reduces the "hey, I did that and it didn't work on my machine" problems. 

## Install a VE with PyEnv

1. Install pyenv (I installed using HomeBrew: [https://github.com/pyenv/pyenv#homebrew-in-macos](https://github.com/pyenv/pyenv#homebrew-in-macos))  
2. Install pyenv virtual env plugin (again, I installed with HomeBrew: [https://github.com/pyenv/pyenv-virtualenv#installing-with-homebrew-for-macos-users](https://github.com/pyenv/pyenv-virtualenv#installing-with-homebrew-for-macos-users))  
3. Using pyenv in the terminal, install the version of python you want it use.  
        Useful commands:  
        * `pyenv install <python version>` For example: `pyenv install 3.11.5` installs python v3.11.5  
        * `pyenv versions` - reports versions of python you have already installed thru pyenv (*note: will not report any installed on machine that were NOT installed with pyenv*)  
        * `pyenv install --list` (reports list of versions not yet installed but available thru pyenv)  
4. Create a VE for the version of python you want to use:  
        `pyenv virtualenv <version of python - must have been installed thru pyenv> <name of venv you want to create>` - eg, `pyenv virtualenv 3.11.5 ve-3.11.5` creates a VE called "ve-3.11.5" that uses python 3.11.5 with the following path: `.pyenv/versions/3.11.5/envs/ve-3.11.5`  
5. *(optional)* Set your VE to activate any time you navigate to your project folder in the terminal:
        In your terminal, change to the project directory you created (eg, my directory is `Documents/notes/midrc/midrc-344`)  
        `pyenv local <name of venv>` - eg, `pyenv local ve-3.11.5`  
        *Note: you will only need to do this once. Thereafter, it will automatically activate when you go to the project folder or any folder within it*
        *Note2: if you ever need to un-set this, you can run `pyenv local --unset`*
7. Be sure you know what's installed in your VE:  
        If it's a new VE, there shouldn't be anything installed. But, especially if it's been used before, you can use `pip freeze` to report what's installed in the VE

##  Install a VE with virtualenv

*Note: if you do not already have virtualenv installed, run `pip install virtualenv` before you proceed with these instructions.*

### Summary

1. Make a directory for your virtual enviroments to live (`mkdir virtalenvs`) *whoops, I misspelled "virtual" in my directory name*
2. Move to that directory (`cd virtalenvs`)
3. Create a virtual environment in that directory (`virtalenv -p <python version, eg "python3.9"> <VE name, eg "mkdocs">`) and verify it's there (`ls` and verify VE name is listed)
4. From within your virtualenvs directory, activate the virtual environment (`source mkdocs/bin/activate`) - after, note change from `(base)` to `(<VE name>) (base)`
5. Install the appropriate programs in your virtual environment (`pip install <your stuff, eg "mkdocs-material">`)
6. You can verify what's installed (`pip freeze`)

### Detailed walkthrough

1. Create a new local directory (`mkdir`) for your virtual environments, if you don't already have one. My directory is called "virtalenvs" because I wasn't paying close enough attention to spelling.
   
     ```
     (base) saravolkdegarcia@Saras-MBP ~ % mkdir virtalenvs
     ```

2. Move to your VE directory (`cd`). Notice that it now says the name of your VE directory in front of the %, indicating your move was successful.

     ```
     (base) saravolkdegarcia@Saras-MBP ~ % cd virtalenvs 
     (base) saravolkdegarcia@Saras-MBP virtalenvs %
     ```

3. Use `virtualenv` to create a new virtual environment in your VE directory. Use `-p` to indicate that it's a Python environment. You can specify what version of Python you want to use - I'm specifying `python3.9`. Finally, append the name of your VE (here, `mkdocs`).
   
     You can verify this was created with the `ls` command, which will list all the directories/VEs in the current directory. Here we see that "mkdocs" is present, so we know we were successful.

        ```
        (base) saravolkdegarcia@Saras-MBP virtalenvs % virtualenv -p python3.9 mkdocs
        created virtual environment CPython3.9.12.final.0-64 in 429ms
        creator CPython3Posix(dest=/Users/saravolkdegarcia/virtalenvs/mkdocs, clear=False, no_vcs_ignore=False, global=False)
        seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/saravolkdegarcia/Library/Application Support/virtualenv)
        added seed packages: pip==22.2.2, setuptools==65.3.0, wheel==0.37.1
        activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
         
        (base) saravolkdegarcia@Saras-MBP virtalenvs % ls
        mkdocs
        ```

4. Now, activate your virtual environment using `source <VE name>/bin/activate`. Since I was using the VE named mkdocs, I used `source mkdocs/bin/activate`. After you activate, note that the beginning of your location will change from `(base)` to `(<VE name>) (base)`

        ```
        (base) saravolkdegarcia@Saras-MBP virtalenvs % source mkdocs/bin/activate
        (mkdocs) (base) saravolkdegarcia@Saras-MBP virtalenvs %
        ```

5. Install the appropriate programs in your virtual environment (`pip install <your stuff, eg "mkdocs-material">`)

        ```
        (mkdocs) (base) saravolkdegarcia@Saras-MBP virtalenvs % pip install mkdocs-material
        Collecting mkdocs-material
        Using cached mkdocs_material-8.5.6-py3-none-any.whl (7.5 MB)
        Collecting mkdocs-material-extensions>=1.0.3
          Using cached mkdocs_material_extensions-1.0.3-py3-none-any.whl (8.1 kB)
        Collecting mkdocs>=1.4.0
          Using cached mkdocs-1.4.0-py3-none-any.whl (3.7 MB)
        Collecting pygments>=2.12
          Using cached Pygments-2.13.0-py3-none-any.whl (1.1 MB)
        Collecting requests>=2.26
          Using cached requests-2.28.1-py3-none-any.whl (62 kB)
        Collecting pymdown-extensions>=9.4
          Using cached pymdown_extensions-9.6-py3-none-any.whl (218 kB)
        Collecting jinja2>=3.0.2
          Using cached Jinja2-3.1.2-py3-none-any.whl (133 kB)
        Collecting markdown>=3.2
          Downloading Markdown-3.4.1-py3-none-any.whl (93 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 93.3/93.3 kB 2.0 MB/s eta 0:00:00
        Collecting MarkupSafe>=2.0
          Downloading MarkupSafe-2.1.1-cp39-cp39-macosx_10_9_x86_64.whl (13 kB)
        Collecting importlib-metadata>=4.4
          Downloading importlib_metadata-5.0.0-py3-none-any.whl (21 kB)
        Collecting packaging>=20.5
          Downloading packaging-21.3-py3-none-any.whl (40 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.8/40.8 kB 5.7 MB/s eta 0:00:00
        Collecting watchdog>=2.0
          Downloading watchdog-2.1.9-cp39-cp39-macosx_10_9_x86_64.whl (87 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 87.5/87.5 kB 12.0 MB/s eta 0:00:00
        Collecting mergedeep>=1.3.4
          Downloading mergedeep-1.3.4-py3-none-any.whl (6.4 kB)
        Collecting click>=7.0
          Downloading click-8.1.3-py3-none-any.whl (96 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.6/96.6 kB 4.2 MB/s eta 0:00:00
        Collecting ghp-import>=1.0
          Downloading ghp_import-2.1.0-py3-none-any.whl (11 kB)
        Collecting pyyaml-env-tag>=0.1
         Downloading pyyaml_env_tag-0.1-py3-none-any.whl (3.9 kB)
        Collecting PyYAML>=5.1
          Using cached PyYAML-6.0-cp39-cp39-macosx_10_9_x86_64.whl (197 kB)
        Collecting markdown>=3.2
          Downloading Markdown-3.3.7-py3-none-any.whl (97 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 97.8/97.8 kB 4.2 MB/s eta 0:00:00
        Collecting idna<4,>=2.5
          Using cached idna-3.4-py3-none-any.whl (61 kB)
        Collecting charset-normalizer<3,>=2
          Using cached charset_normalizer-2.1.1-py3-none-any.whl (39 kB)
        Collecting urllib3<1.27,>=1.21.1
          Using cached urllib3-1.26.12-py2.py3-none-any.whl (140 kB)
        Collecting certifi>=2017.4.17
          Downloading certifi-2022.9.24-py3-none-any.whl (161 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 161.1/161.1 kB 4.7 MB/s eta 0:00:00
        Collecting python-dateutil>=2.8.1
          Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 247.7/247.7 kB 6.9 MB/s eta 0:00:00
        Collecting zipp>=0.5
          Downloading zipp-3.9.0-py3-none-any.whl (5.8 kB)
        Collecting pyparsing!=3.0.5,>=2.0.2
          Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
             ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.3/98.3 kB 4.0 MB/s eta 0:00:00
        Collecting six>=1.5
          Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
        Installing collected packages: zipp, watchdog, urllib3, six, PyYAML, pyparsing, pygments, mkdocs-material-extensions, mergedeep, MarkupSafe, idna, click, charset-normalizer, certifi, requests, pyyaml-env-tag, python-dateutil, packaging, jinja2, importlib-metadata, markdown, ghp-import, pymdown-extensions, mkdocs, mkdocs-material
        Successfully installed MarkupSafe-2.1.1 PyYAML-6.0 certifi-2022.9.24 charset-normalizer-2.1.1 click-8.1.3 ghp-import-2.1.0 idna-3.4 importlib-metadata-5.0.0 jinja2-3.1.2 markdown-3.3.7 mergedeep-1.3.4 mkdocs-1.4.0 mkdocs-material-8.5.6 mkdocs-material-extensions-1.0.3 packaging-21.3 pygments-2.13.0 pymdown-extensions-9.6 pyparsing-3.0.9 python-dateutil-2.8.2 pyyaml-env-tag-0.1 requests-2.28.1 six-1.16.0 urllib3-1.26.12 watchdog-2.1.9 zipp-3.9.0
        ```
## Verify what's installed with `pip freeze`
If you want, you can verify what's installed in your VE using `pip freeze`. If you want to make a record of what's installed, you can send the list to a requirements.txt. 

        ```
        (mkdocs) (base) saravolkdegarcia@Saras-MBP virtalenvs % pip freeze
        certifi==2022.9.24
        charset-normalizer==2.1.1
        click==8.1.3
        ghp-import==2.1.0
        idna==3.4
        importlib-metadata==5.0.0
        Jinja2==3.1.2
        Markdown==3.3.7
        MarkupSafe==2.1.1
        mergedeep==1.3.4
        mkdocs==1.4.0
        mkdocs-material==8.5.6
        mkdocs-material-extensions==1.0.3
        packaging==21.3
        Pygments==2.13.0
        pymdown-extensions==9.6
        pyparsing==3.0.9
        python-dateutil==2.8.2
        PyYAML==6.0
        pyyaml_env_tag==0.1
        requests==2.28.1
        six==1.16.0
        urllib3==1.26.12
        watchdog==2.1.9
        zipp==3.9.0
        ```
