# vscode-fail-example

Example of VSCode Python debugger failing when tests requires custom PWD.

Steps to reproduce:

    1. Use `make init` to create venv in the venv/ directory.
    2. Configure your VSCode to use it as an interpreter.
    3. At the moment, you cannot find any tests in the Test Explorer. Let's fix it by setting in VSCode `python.testing.cwd` to the `subproject/theproject` directory.
    4. Now, you can open test explorer and run tests. It should pass.
    5. Let's try to debug the test. Apparently, you cannot, and in `output/Python` you see something like: `[ERROR...] [object Object] [object Object]`

Steps to debug the troubles:

    1. Try run a test debug, then look into Output/Python window, find a line DAP Server launched with command ...
    2. Basing on this path, open the folder pythonFiles in the extension's dir, and first do following:
            in lib/python/debugpy/adapter/__main__.py find the line about 44, and force the log.log_dir to a chosen writable directory,
            in visualstudio_py_testlauncher.py look into the main() and in the main try/except block, before the finally add the following:

        except Exception as err:
            errorMessage = traceback.format_exc()
            print(errorMessage)

    3. Now run tests once more, and in the selected logs directory, in the debugpy.adapter-xxx.log file, look for "category": "stdout". You will see outputs from the test runner.
    4. Use your magic power and debug, add prints etc. until you discover the issue.
