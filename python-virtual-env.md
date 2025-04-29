# Using Python Virtual Environments (venv) in VSCode

Step-by-step guide to create, activate, rename, register, and delete Python virtual environments in VSCode with Jupyter support, including how to fix script execution errors in PowerShell.

---

## 1. Create a virtual environment from the VSCode UI

1. Open your project or folder in VSCode.
2. Open the command palette with `Ctrl+Shift+P` or `F1`.
3. Type: `Python: Create Environment` and select it.
4. Choose:
   - **Venv** as the environment type.
   - Installed Python version.
   - Target folder (default: `.venv`, but you can rename it).

VSCode automatically creates and configures the environment.

---

## 2. Activate the virtual environment from the VSCode terminal

### ✅ Automatic activation

- If you select the interpreter from `Python: Select Interpreter`, VSCode will activate the virtual environment automatically when you open a new terminal.

### ❌ If **it doesn't activate automatically**, do it manually:

#### Windows PowerShell:

```powershell
.\.venv\Scripts\Activate
```

#### CMD:

```cmd
.ven\Scripts\activate.bat
```

#### Linux/macOS:

```bash
source .venv/bin/activate
```

---

## 3. Script execution error (PowerShell)

If you see an error like this:

```powershell
.venv\Scripts\Activate.ps1 : The file cannot be loaded ... because script execution is disabled...
```

### ✅ Safe solution (only for this session):

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

- Type `Y` when prompted.
- Then activate the venv with:

```powershell
.\.venv\Scripts\Activate
```

### ⚠️ Permanent alternative (less secure):

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## 4. Rename the venv

1. Close VSCode.
2. Rename the virtual environment folder (`.venv` → `.venv-name`, for example).
3. Reopen your project in VSCode.
4. Select the correct interpreter from:  
   `Ctrl+Shift+P > Python: Select Interpreter`.

---

## 5. Register the venv as a Jupyter kernel

After creating or renaming the `venv`, run this **inside the activated venv**:

```bash
pip install ipykernel
python -m ipykernel install --user --name .venv --display-name "Python (.venv)"
```

> This makes Jupyter (and VSCode) show it as a kernel option.

---

## 6. Delete a venv

- Simply **delete the virtual environment folder** using File Explorer or `rm -r` / `del`.
- If you registered it in Jupyter, remove the kernel with:

```bash
jupyter kernelspec uninstall .venv
```

---

## 🧠 Additional tips

- To exit the virtual environment: `deactivate`
- To always activate it automatically in VSCode:

```json
// settings.json
"python.terminal.activateEnvironment": true
```

---

## ✅ Required tools

Make sure you have the following installed:

- Python 3.7+
- Python extension in VSCode
- Jupyter extension in VSCode
- Jupyter:
  ```bash
  pip install jupyter
  ```

---

And that’s it! Now you can work with virtual environments and Jupyter in an organized and professional way from VSCode 🎉
