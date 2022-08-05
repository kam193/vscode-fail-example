# vscode-fail-example

Example of VSCode Python debugger failing when tests requires custom PWD.

Steps to reproduce:

    1. Use `make init` to create venv in the venv/ directory.
    2. Configure your VSCode to use it as an interpreter.
    3. At the moment, you cannot find any tests in the Test Explorer. Let's fix it by setting in VSCode `python.testing.cwd` to the `subproject/theproject` directory.
    4. Now, you can open test explorer and run tests. It should pass.
    5. Let's try to debug the test. Apparently, you cannot, and in `output/Python` you see something like: `[ERROR...] [object Object] [object Object]`