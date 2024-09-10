# Setting_up_env_path_mac_os

### For `zsh` (default on macOS Catalina and later):

1. **Open Terminal**.

2. **Edit `.zshrc`**:
   ```bash
   nano ~/.zshrc
   ```

3. **Add these lines**:
   ```bash
   export ANDROID_HOME=$HOME/Library/Android/sdk
   export PATH=$PATH:$ANDROID_HOME/platform-tools
   export PATH=$PATH:$ANDROID_HOME/emulator
   ```

4. **Save and exit** (press `Ctrl + X`, then `Y`, and `Enter`).

5. **Apply changes**:
   ```bash
   source ~/.zshrc
   ```

### For `bash` (default on older macOS):

1. **Open Terminal**.

2. **Edit `.bash_profile`**:
   ```bash
   nano ~/.bash_profile
   ```

3. **Add these lines**:
   ```bash
   export ANDROID_HOME=$HOME/Library/Android/sdk
   export PATH=$PATH:$ANDROID_HOME/platform-tools
   export PATH=$PATH:$ANDROID_HOME/emulator
   ```

4. **Save and exit** (press `Ctrl + X`, then `Y`, and `Enter`).

5. **Apply changes**:
   ```bash
   source ~/.bash_profile
   ```

To check if it worked, run:
```bash
echo $ANDROID_HOME
echo $PATH
```
