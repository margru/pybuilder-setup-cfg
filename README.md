# PyBuilder setup.cfg plugin

[PyBuilder](http://pybuilder.github.io/) plugin for getting various information from the setup.cfg file.

## How to use it

In your `build.py`:

```
use_plugin("pypi:pybuilder_setup_cfg")
```

The setup_cfg plugin works as an initializer. You do not have to do anything else. 

It reads the following settings from the setup.cfg file (or environment variables) and set project properties accordingly:
- name ($PYB_SCFG_NAME, metadata.name)
- version ($PYB_SCFG_VERSION, metadata.version)
- package_data (files.package_data)
- default_task (tool:pybuilder.default_task - might be a list)
- distutils_commands ($PYB_SCFG_DISTUTILS_COMMANDS, tool:pybuilder.distutils_commands - might be a list)
- distutils_upload_repository ($PYB_SCFG_UPLOAD_REPOSITORY, tool:pybuilder.distutils_upload_repository) - if environment variable `TWINE_REPOSITORY_URL` is set, it will be used anyway and the `distutils_upload_repository` will be ignored 
- distutils_cython_ext_modules (tool:pybuilder.cython_include_modules and tool:pybuilder.cython_exclude_modules)
- distutils_cython_remove_python_sources (tool:pybuilder.cython_remove_python_sources)
- copy_resources_glob (tool:pybuilder.copy_resources_glob) + adding files from package_data
- pytest_coverage_break_build_threshold ($PYB_SCFG_PYTEST_COVERAGE_BREAK_BUILD_THRESHOLD, tool:pytest.coverage_break_build_threshold)
    
Cython-related stuff is not integrated in official PyBuilder, there is a PR #640 for that.