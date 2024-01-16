> **Feel free to clone this repo and try this for yourself. If you don't have linux, try installing virtualbox, install ubuntu server and give this a go!**

# Guide to Installing pyenv on Debian Linux Distros

**Update and Install Dependencies**:
First, update your package list and install dependencies required for `pyenv` and Python build:

```bash
sudo apt update

sudo apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev git
```

1. **Install** `pyenv`:
   The best way to install `pyenv` is to use its installer script. You can download and run it with this command:

   ```bash
   curl https://pyenv.run | bash
   ```

2. **Configure Shell Environment**:
   After installing `pyenv`, you need to add `pyenv` to your shell's environment variables. For this, you'll need to edit your shell configuration file (like `~/.bashrc`, `~/.zshrc`, etc.). If you're using Bash, use:

   ```bash
   echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
   echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
   echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
   echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
   ```

   After adding these lines, apply the changes with:

   ```bash
   source ~/.bashrc
   ```

3. **Restart Your Shell**:
   To make sure all changes take effect, you may need to restart your shell or log out and back in.
4. **Install Python Versions**:
   With `pyenv` installed, you can install different versions of Python. For example, to install Python 3.8.0, use:

   ```bash
   pyenv install 3.8.0
   ```

   You can list all available versions with `pyenv install --list`.

5. **Set Global Python Version**:
   Set a global Python version for your entire system with `pyenv global`. For example:

   ```bash
   pyenv global 3.8.0
   ```

   This sets Python 3.8.0 as the default version when you run `python` or `python3`.

6. **Verification**:
   Finally, verify that the new version is being used by running:

   ```bash
   python --version
   ```

---

# Guide to Using pipenv for Python Project Management

### Installing pipenv

1. **Ensure the Correct Python Version is Active**:

   - Check the active Python version installed with `pyenv`:

     ```bash
     python --version
     ```

     or

     ```bash
     pyenv versions
     ```

2. **Update** `pip` (optional but recommended):

   - Keep `pip` up-to-date before installing new packages:

     ```bash
     python -m pip install --upgrade pip
     ```

3. **Install** `pipenv`:

   - Install `pipenv` using `pip`:

     ```bash
     python -m pip install pipenv
     ```

   **Add to PATH**:

   - Once you've located the `pipenv` executable, you need to add its directory to your system's PATH environment variable.
   - Edit your shell's profile script (like `~/.bashrc`, `~/.bash_profile`, or `~/.zshrc`, depending on your shell). Add the following line at the end of the file:
     ```bash
     export PATH="$HOME/.pyenv/versions/3.12.0/bin:$PATH"
     ```
   - Make sure to replace `3.12.0` with the actual version directory if it's different.

   **Reload Your Profile**:

   - To apply the changes, reload your profile. For example, if you're using bash, you can run:
     ```bash
     source ~/.bashrc
     ```
   - Or simply close and reopen your terminal.

4. **Verify the Installation**:

   - Confirm that `pipenv` is installed:

     ```bash
     pipenv --version
     ```

5. **Configure** `pipenv` for Specific Python Version:

   - Specify the Python version for a new project with `pipenv`:

     ```bash
     pipenv --python 3.8
     ```

### Using `pipenv` with `requirements.txt`

- Install dependencies from `requirements.txt` using `pipenv`:

  ```bash
  pipenv install -r requirements.txt
  ```

---

### Using `Pipfile` with `pipenv`

- `Pipfile` is used by `pipenv` as a replacement for `requirements.txt` to manage project dependencies.
- When you run `pipenv install`, it automatically creates a `Pipfile` if one doesn't exist.

### Creating a New Project with `Pipfile`

1. **Initialize the Environment**:

   - Start a new project with:

     ```bash
     pipenv --python 3.8
     ```

   - This command creates a `Pipfile` for your project.

2. **Install Packages**:

   - Install a new package and add it to your `Pipfile`:

     ```bash
     pipenv install package_name
     ```

### Managing Dependencies

- **Adding a Dependency**:

  - Add a package to your `Pipfile` and install it:

    ```bash
    pipenv install package_name
    ```

- **Removing a Dependency**:

  - Remove a package and update your `Pipfile`:

    ```bash
    pipenv uninstall package_name
    ```

- **Locking Dependencies**:

  - Generate a `Pipfile.lock` to lock dependencies to specific versions:

    ```bash
    pipenv lock
    ```

  - `Pipfile.lock` ensures that the same versions of the dependencies are used every time you install them.

### Activation and Deactivation of the Virtual Environment

- **Activating the Environment**:

  - Before working on your project, activate the `pipenv` environment:

    ```bash
    pipenv shell
    ```

- **Deactivating the Environment**:

  - When done, exit the environment:

    ```bash
    exit
    ```

## Notes

- `pipenv` simplifies the process of managing virtual environments and dependencies in Python projects.
- The use of `Pipfile` and `Pipfile.lock` ensures consistent and repeatable package installations.
