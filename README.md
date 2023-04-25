# PyBuilder setup.cfg plugin

[PyBuilder](http://pybuilder.github.io/) plugin for getting various information from the setup.cfg file. Tested for PyBuilder version 0.11.X.

## How to use it

In your `build.py`:

```
use_plugin("pypi:pybuilder_setup_cfg")
```

**IMPORTANT** Use this plugin as the first one as it's getting basic data from the `setup.cfg` that may be overwritten/adjusted later on. It may not work properly if not loaded as the first plugin in your project.

The setup_cfg plugin works as an initializer. You do not have to do anything else. 

It reads the following settings from the setup.cfg file (or from environment variables) and set project properties accordingly:
- name
  - envvar: PYB_SCFG_NAME
  - section: metadata
  - option: name
- version
  - envvar: PYB_SCFG_VERSION
  - section: metadata
  - option: name
- package_data
  - description: list of items where each item is a whitespace or comma separated list of file patterns to include
  - section: options.package_data (standard location and format)

    OR

  - section: files
  - option: package_data
- default_task
  - description: list of default task names
  - section: tool:pybuilder
  - option: default_task
- distutils_commands
  - description: list of distutils commands to execute
  - envvar: PYB_SCFG_DISTUTILS_COMMANDS
  - section: tool:pybuilder
  - option: distutils_commands
- distutils_upload_repository 
  - envvar: PYB_SCFG_UPLOAD_REPOSITORY
  - section: tool:pybuilder
  - option: distutils_upload_repository
  - **note**: if environment variable `TWINE_REPOSITORY_URL` is set, it will be used anyway and the _distutils_upload_repository_ will be ignored
- distutils_cython_ext_modules (*)
  - description: lists of file patterns
  - section: tool:pybuilder
  - option: cython_include_modules AND cython_exclude_modules
- distutils_cython_remove_python_sources (*)
  - section: tool:pybuilder
  - option: cython_remove_python_sources
- distutils_cython_compiler_directives
  - section: tool:pybuilder.cython_compiler_directives
  - description: section items will be passed to cythonize
    as compiler_directives dictionary
- copy_resources_glob
  - section: tool:pybuilder
  - option: copy_resources_glob
  - **note**: it's adding files from _package_data_ automatically
- pytest_coverage_break_build_threshold
  - envvar: PYB_SCFG_PYTEST_COVERAGE_BREAK_BUILD_THRESHOLD
  - section: coverage:report (standard location)
  - option: fail_under

    OR

  - section: tool:pytest
  - option: coverage_break_build_threshold
- pytest_coverage_html
  - description: possible values: True | False
  - section: tool:pytest
  - option: coverage_html
- pytest_coverage_annotate
  - description: possible values: True | False
  - section: tool:pytest
  - option: coverage_annotate
- scm_ver_version_scheme
  - description: to be used by _pybuilder-scm-ver-plugin_; possible values: see _setuptools_scm_ package
  - section: tool:setuptools_scm
  - option: version_scheme
- scm_ver_local_scheme
  - description: to be used by _pybuilder-scm-ver-plugin_; possible values: see _setuptools_scm_ package
  - section: tool:setuptools_scm
  - option: local_scheme

(*) Cython-related stuff is not integrated in official PyBuilder, there is a PR [#640](https://github.com/pybuilder/pybuilder/pull/640) for that.