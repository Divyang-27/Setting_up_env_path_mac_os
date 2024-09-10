

### WebDriverIO Mobile App Testing Setup on macOS

#### Prerequisites:
1. **Node.js and npm**: Download and install Node.js from [nodejs.org](https://nodejs.org), which includes npm.
2. **Visual Studio Code**: Install Visual Studio Code from [code.visualstudio.com](https://code.visualstudio.com).
3. **Android Studio**: Download and install Android Studio from [developer.android.com/studio](https://developer.android.com/studio).

#### Step-by-Step Configuration:

1. **Install Android Studio and Set Environment Variables**:
   - **Download and install** Android Studio.
   - **Set environment variables**:
     1. **Open Terminal**.
     2. **Edit `.zshrc`** (for zsh users) or `.bash_profile` (for bash users):
        ```bash
        nano ~/.zshrc  # or nano ~/.bash_profile
        ```
     3. **Add these lines** to set up the Android SDK and JDK paths:
        ```bash
        # Android SDK
        export ANDROID_HOME=$HOME/Library/Android/sdk
        export PATH=$PATH:$ANDROID_HOME/platform-tools
        export PATH=$PATH:$ANDROID_HOME/emulator

        # JDK
        export JAVA_HOME=$(/usr/libexec/java_home)
        export PATH=$PATH:$JAVA_HOME/bin
        ```
     4. **Save and exit** (press `Ctrl + X`, then `Y`, and `Enter`).
     5. **Apply changes**:
        ```bash
        source ~/.zshrc  # or source ~/.bash_profile
        ```

2. **Create and Run an Android Emulator**:
   - **Open Android Studio** and go to AVD Manager:
     - Click on **Configure** > **AVD Manager**.
     - Select **Create Virtual Device**.
     - Choose **Pixel 8a** and select **Oreo API Level 26**.
   - **Start the emulator**:
     ```bash
     cd $ANDROID_HOME/emulator
     ./emulator -avd <Your_Emulator_Name>
     ```

3. **Install Node.js and Appium**:
   - **Verify Node.js and npm**:
     ```bash
     node -v
     npm -v
     ```
   - **Install Appium globally**:
     ```bash
     npm install -g appium@next
     ```
   - **Install Appium Doctor**:
     ```bash
     npm install -g appium-doctor
     ```
   - **Run Appium Doctor** (optional):
     ```bash
     appium-doctor --android
     ```

4. **Setup WebDriverIO in Visual Studio Code**:
   - **Open Visual Studio Code** and create a new project folder.
   - **Open Terminal** in VS Code and run:
     ```bash
     npm init wdio webdriverio-appium-v8 --save-dev
     ```
   - **Follow the prompts**:
     - **Type of testing**: E2E Testing - Web or Mobile Applications.
     - **Automation Backend**: On my local machine.
     - **Environment to automate**: Mobile - Native, Hybrid, and Web Apps.
     - **Mobile Environment**: Android.
     - **Automation Framework**: Mocha.
     - **Add services**: Appium.

5. **Emulator and APK Setup**:
   - **Create a script** to start your emulator (e.g., `Shiva.sh`):
     ```bash
     cd $ANDROID_HOME/emulator
     ./emulator -avd <Your_Emulator_Name>
     ```
   - **Install an APK on the emulator**:
     - Copy your APK to `$ANDROID_HOME/platform-tools`.
     - Open Terminal from this directory and run:
       ```bash
       adb install <name_of_apk.apk>
       ```

6. **Configure WebDriverIO for Mobile Testing**:
   - **Update `wdio.conf.js`**:
     ```javascript
     const path = require('path');

     exports.config = {
       specs: [
         './test/specs/**/*.js'
       ],
       capabilities: [{
         'appium:platformName': 'Android',
         'appium:deviceName': 'Shiva_Pixel',
         'appium:automationName': 'UiAutomator2',
         'appium:noReset': true,
         'appium:app': path.join(process.cwd(), "/app/android/YourApp.apk")
       }],
       services: [
         ['appium', {
           command: 'appium',
         }]
       ]
     };
     ```

   - **Update `package.json`**:
     ```json
     "scripts": {
       "wdio": "wdio run ./wdio.conf.js"
     }
     ```

7. **Create Test Files**:
   - **Folder structure**:
     ```
     test/
     └── specs/
         └── example.test.js
     ```

8. **Running Tests**:
   - **Run your tests** in the VS Code terminal:
     ```bash
     npx wdio wdio.conf.js
     ```

9. **Using Appium Inspector**:
   - **Download and install** Appium Inspector from its [official site](https://appium.io).
   - **Configure and start a session**:
     - **Platform Name**: Android
     - **Device Name**: Shiva_Pixel
     - **App Package**: (Get this from the APK info app)
     - **App Activity**: (Choose from available activities)
     - **Automation Name**: UiAutomator2
   - **Save and start the session**.

