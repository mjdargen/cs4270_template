# Table of Contents

- [Setting Up Local Environment](#setting-up-local-environment)

  - [Step 1: Install Liberica Full Java JDK with JavaFX](#step-1-install-liberica-full-java-jdk-with-javafx)
  - [Step 2: Install VS Code](#step-2-install-vs-code)
  - [Step 3: Install VS Code Java Extensions](#step-3-install-vs-code-java-extensions)
  - [Step 4: Disable AI](#step-4-disable-ai)
  - [Step 5: Setup Maven](#step-5-setup-maven)
  - [Step 6: Install Git](#step-6-install-git)
  - [Step 7: Create a GitHub Account](#step-7-create-a-github-account)
  - [Step 8: Authenticate Git & GitHub in VS Code](#step-8-authenticate-git--github-in-vs-code)

- [Creating a Java Project](#creating-a-java-project)

  - [Option 1: Forking My Template Repository](#option-1-forking-my-template-repository)
  - [Option 2: Creating a Java Project with No Dependencies](#option-2-creating-a-java-project-with-no-dependencies)
  - [Option 3: Creating a Java Project with Maven](#option-3-creating-a-java-project-with-maven)
  - [Double-Check VS Code Java Runtime](#double-check-vs-code-java-runtime)

- [Connecting Your Java Project to GitHub](#connecting-your-java-project-to-github)

  - [Independent Project](#independent-project)
  - [Shared Repository (Team Project)](#shared-repository-team-project)

- [Collaborating with VS Code via Git & Live Share](#collaborating-with-vs-code-via-git--live-share)
  - [Synchronous Work: Live Share](#synchronous-work-live-share)
  - [Asynchronous Work: Git](#asynchronous-work-git)
  - [Good Habits Checklist](#good-habits-checklist)

<br><br>

# Setting Up Local Environment

## Step 1: Install Liberica Full Java JDK with JavaFX

**Note:** there are many different flavors of JDK environments. We will be using the following because it includes **JavaFX**, which is required for graphical applications.

If you already have another JDK installed, that’s fine. You can still install this one and later configure VS Code to use the correct Java runtime.

[https://bell-sw.com/pages/downloads](https://bell-sw.com/pages/downloads)

1. Go to the page above.
2. Click the tab for the latest **LTS (Long-Term Support)** release (for example, Java 21 LTS).
3. Scroll down to the section for your operating system.
4. Open the “Package” dropdown and **select “Full JDK”** (this is the one that includes JavaFX).
5. On **Windows**, download the `.msi` installer and run it.On **Mac**, download the `.dmg` file and run it.

![image.png](https://ncssm.instructure.com/courses/12681/files/2673932/preview)

**STOP! Are you sure you downloaded the FULL JDK?** Every year, someone downloads the Standard or Lite JDK without JavaFX. Make sure the filename or package description says **“Full JDK with JavaFX”** before continuing.

## Step 2: Install VS Code

You may use any editor you prefer, but for this course, **instructions and troubleshooting will assume VS Code**.

[https://code.visualstudio.com/](https://code.visualstudio.com/)

Run the installer for your system and launch the editor once it’s installed.

## Step 3: Install VS Code Java Extensions

Open VS Code, go to the **Extensions** tab on the left sidebar, and search for and install the following:

- (Required) **VS Code Java Extension Pack**  
  [https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
- (Required) **Live Share**[https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
- (Optional) **Code Spell Checker**[https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

## Step 4: Disable AI

You **must** disable GitHub Copilot and other AI features in VS Code for this course.

1. Click the **gear icon** (Settings) in the lower-left corner, or press **Ctrl/Cmd + ,**.
2. In the search bar, type “chat disable.”
3. Enable the option **“Disable AI features.”**

![Screenshot 2025-10-23 162205.png](https://ncssm.instructure.com/courses/12681/files/2785955/preview)

Or edit your user `settings.json` directly:

```
"chat.disableAIFeatures": true
```

## Step 5: Setup Maven

Maven manages external Java libraries (dependencies). It downloads them automatically into your project based on your `pom.xml` configuration file. VS Code’s Java extensions integrate Maven directly, allowing you to search for dependencies from **Maven Central**.

#### Windows

1. Open the Start menu, search for **PowerShell**, right-click, and select **Run as administrator**.
2. Copy and paste the following command. When it completes, you should see Maven and Java version information.

```ps
$MavenUrl = "https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.zip"; $MavenZipPath = "$env:USERPROFILE\Downloads\apache-maven-3.9.11-bin.zip"; Invoke-WebRequest -Uri $MavenUrl -OutFile $MavenZipPath; $ProgramFilesPath = [System.Environment]::GetFolderPath('ProgramFiles'); $MavenExtractPath = "$ProgramFilesPath\apache-maven"; Expand-Archive -Path $MavenZipPath -DestinationPath $MavenExtractPath; $MavenBinPath = "$MavenExtractPath\apache-maven-3.9.11\bin"; $currentPath = [System.Environment]::GetEnvironmentVariable("Path", [System.EnvironmentVariableTarget]::Machine); if (-not $currentPath.Contains($MavenBinPath)) { $newPath = $currentPath + ";" + $MavenBinPath; [System.Environment]::SetEnvironmentVariable("Path", $newPath, [System.EnvironmentVariableTarget]::Machine) }; [System.Environment]::SetEnvironmentVariable("Path", [System.Environment]::GetEnvironmentVariable("Path", [System.EnvironmentVariableTarget]::Machine), [System.EnvironmentVariableTarget]::Process); mvn -v
```

#### Mac

Open **Terminal**, then run:

```bash
curl -L https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.tar.gz -o ~/Downloads/apache-maven-3.9.11-bin.tar.gz && sudo mkdir -p /usr/local/apache-maven && sudo tar -xzvf ~/Downloads/apache-maven-3.9.11-bin.tar.gz -C /usr/local/apache-maven --strip-components=1 && if ! grep -q "/usr/local/apache-maven/bin" ~/.bash_profile; then echo "export PATH=\$PATH:/usr/local/apache-maven/bin" >> ~/.bash_profile && source ~/.bash_profile; fi && if [ -f "~/.zshrc" ] && ! grep -q "/usr/local/apache-maven/bin" ~/.zshrc; then echo "export PATH=\$PATH:/usr/local/apache-maven/bin" >> ~/.zshrc && source ~/.zshrc; fi && mvn -v
```

#### Manual Installation (if needed)

If the automated commands fail:

1. Go to [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)
2. Download the **Binary zip archive**.
3. Extract it and move the folder to a stable location (e.g. `C:\Program Files` on Windows or `/usr/local` on Mac).
4. Add its `bin` directory to your PATH.
   - Windows: Edit System Environment Variables → PATH
   - Mac/Linux: `export PATH=$PATH:/path/to/apache-maven/bin`

Run `mvn -v` again to confirm installation.

## Step 6: Install Git

[https://git-scm.com/install/](https://git-scm.com/install/)

Git is a **version control system**. It tracks changes, allows collaboration, and lets you revert to previous versions if something breaks. Think of it as Google Docs for code, but with files and folders instead of text documents.

Run `git --version` after installation to verify it’s installed correctly.

## Step 7: Create a GitHub Account

If you don’t already have one: [https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github)

Use your school email address if possible.

## Step 8: Authenticate Git & GitHub in VS Code

VS Code integrates Git and GitHub directly.

1. Open VS Code → Source Control tab (the branch icon on the sidebar).
2. Click “Sign in to GitHub.”
3. Follow the prompts in your browser to authorize VS Code.

Once complete, VS Code should automatically detect your GitHub repositories.

If you see errors when pushing code, configure Git manually:

```
git config --global user.name "YourGitHubUsername"
git config --global user.email "youremail@example.com"
```

If prompted for authentication when pushing to GitHub, **use a Personal Access Token (PAT)** instead of your password (GitHub no longer accepts passwords).  
Follow this guide to create one: [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

<br><br>

# Creating a Java Project

## Option 1: Forking My Template Repository

If you want to start from a fully configured Java + Maven project structure for this course, you can fork my template repository instead of creating a project from scratch.

**Repository link:** [https://github.com/mjdargen/cs4270_template](https://github.com/mjdargen/cs4270_template)

1. Visit the template repository link above.
2. Click the **Fork** button in the top-right corner of the page.
3. Choose your own GitHub account as the destination.
4. Once the fork is created, click the **Code** button on your new fork’s page and copy the **HTTPS** clone URL.
5. In VS Code:
   - Open the **Source Control** panel.
   - Click **Clone Repository**.
   - Paste the URL you copied.
   - Choose a local folder to store the project.

This template already includes:

- A standard Maven project structure (`src/main/java`, `src/test/java`, `pom.xml`)
- JavaFX dependency configuration
- A starter class with a `main()` method to test

## Option 2: Creating a Java Project with No Dependencies

1. Open a new VS Code window.
2. Open the Command Palette (**Ctrl+Shift+P** / **Cmd+Shift+P**).
3. Type and select **Java: Create Java Project**.
4. Choose **No build tools**.
5. Select or create an empty folder and name your project.

VS Code will generate a `src` folder and a sample `App.java` file with a main method. Keep all your source code inside the `src` directory.

## Option 3: Creating a Java Project with Maven

Follow the same process as above, but select **Maven** instead of **No build tools**.

1. Select **No archetype** when prompted.
2. Enter your **group id** (default is fine).
3. Enter your **artifact id**, which becomes your project name.
4. Choose or create a folder to store your project.

When the project is created, VS Code will generate a `pom.xml` file to manage dependencies. You can add dependencies from the **Maven panel** in VS Code or directly in the `pom.xml` file. When you save the file, VS Code will prompt to reload — click **Yes**.

Be careful: not all libraries on Maven Central are trustworthy. Always check the publisher and artifact details before adding dependencies.

## Double-Check VS Code Java Runtime

If your project fails to build or run, make sure VS Code is using the correct JDK:

1. Open the Command Palette (**Ctrl+Shift+P**).
2. Search for **Java: Configure Java Runtime**.
3. Under “Runtime for Projects,” set the **Liberica Full JDK** as the default runtime.

<br><br>

# Connecting Your Java Project to GitHub

## Independent Project

You can initialize your local project as a Git repository and publish it to GitHub directly from VS Code:

1. Open your project in VS Code.
2. Go to the **Source Control** panel.
3. Click **Initialize Repository**.
4. Click **Publish Branch** and sign in to GitHub if prompted.
5. Confirm repository name and visibility.

Your project is now backed up online and ready for version control.

## Shared Repository (Team Project)

1. One partner creates a **GitHub repository** and adds the other as a **collaborator** (Settings → Collaborators → Add by GitHub username).
2. Both partners **clone** the repository into VS Code.
3. Both now have a synchronized copy of the same project.

<br><br>

# Collaborating with VS Code via Git & Live Share

Your goal is to maintain **one shared, up-to-date version** of the project that both partners can open, run, and build from.

Use:

- **Live Share** for **synchronous collaboration** (working at the same time at the same time).
- **Git/GitHub** for **asynchronous collaboration** (working at different times or on different files).

## Synchronous Work: Live Share

Use when you both need to code in real time on the same files.

**Host setup**

1. Open the full project folder in VS Code.
2. Click the **Live Share** button at the bottom of the window.
3. Sign in with your school account if prompted.
4. Send the invite link to your partner.

**Partner setup**

1. In VS Code, click **Join Live Share** and paste the invite link.
2. Both users can now edit files simultaneously.
3. The host’s computer runs and tests the code.

**When finished**

1. The host saves all files (**Ctrl + K, S**) and ends the session.
2. The host commits and pushes the final version to GitHub.

## Asynchronous Work: Git

When working separately, use Git to stay in sync.

**Before starting work**

1. Open VS Code.
2. **Pull** from GitHub to get the latest updates.

**After making changes**

1. Save all files.
2. Stage your changes.
3. Write a short, descriptive commit message (e.g. `added enemy collision logic`).
4. Push your changes to GitHub.

**When your partner updates**

Always **pull** before editing again to merge their latest changes.

## Good Habits Checklist

- Pull before you start working each time.
- Commit and push when you finish.
- Only one partner should push at a time to avoid merge conflicts.
- Use clear commit messages (e.g. `fixed gravity bug`, `added sound manager`).
- Communicate before reorganizing files.
- Keep the repository clean and up to date.
