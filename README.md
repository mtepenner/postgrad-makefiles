#### Overview
This project contains three dedicated Makefiles designed to save time by automating Git versioning, polyglot environment setup, and Linux system hardening. 

#### 1. Git Automation (`git-automation`)
This Makefile automates standard Git revision processes and semantic versioning. It uses a `VERSION` file as the single source of truth to manage release numbers.

**Commands:**
* `make init`: Initializes the repository by creating a `VERSION` file starting at `0.0.0`. If the file already exists, it will notify you without overwriting.
* `make status`: Shows the current git status.
* `make commit MSG="your message"`: Stages all current changes and commits them with the provided message. If no message is provided, it defaults to `"chore: auto-commit updates"`.
* `make patch`: Bumps the patch version number (e.g., `x.y.Z+1`), updates the `VERSION` file using `awk`, creates a release commit, and tags it.
* `make minor`: Bumps the minor version number (e.g., `x.Y+1.0`), updates the `VERSION` file, creates a release commit, and tags it.
* `make major`: Bumps the major version number (e.g., `X+1.0.0`), updates the `VERSION` file, creates a release commit, and tags it.
* `make push`: Pushes commits and tags to the remote repository (`origin HEAD` and `--tags`).

#### 2. Polyglot Language Installer (`language-installer/Makefile`)
This Makefile serves as a Polyglot Developer Environment Installer for Debian/Ubuntu systems.

**Commands:**
* `make install-all`: Updates repositories and sequentially installs C/C++, Python, Node.js, Rust, Go, and Java. Note that after installation, you may need to restart your terminal or source your profile (e.g., `~/.bashrc`) to ensure Rust and Node paths load correctly.
* `make update`: Updates system package repositories via `apt-get`.
* `make install-c`: Installs GCC and Make via the `build-essential` package.
* `make install-python`: Installs Python 3, `pip`, and `venv`.
* `make install-node`: Downloads the official NodeSource setup script and installs the latest Node.js LTS and NPM.
* `make install-rust`: Downloads and runs the official `rustup` script non-interactively to install Rust.
* `make install-go`: Installs Go via the `golang-go` package.
* `make install-java`: Installs the default OpenJDK.

#### 3. Linux System Updater & Security Hardening (`linux-updater/Makefile`)
This Makefile automates system updates, installs essential defensive tools, and configures basic security settings for Debian/Ubuntu systems.

**Commands:**
* `make all`: Runs system updates, installs security tools, configures the firewall, and cleans up unused packages.
* `make update`: Updates package lists, upgrades the system, and performs a distribution upgrade (`dist-upgrade`).
* `make install-security`: Installs a baseline of security software, including UFW (Uncomplicated Firewall), Fail2Ban (prevents brute-force attacks), RKHunter (rootkit scanner), unattended-upgrades (automatic security updates), and libpam-tmpdir (secures temporary directory creation).
* `make configure-security`: Configures essential firewall rules using UFW. It explicitly allows SSH traffic (port 22) to prevent lockouts, sets default policies to deny incoming and allow outgoing traffic, and force-enables the firewall. It also enables and starts the Fail2Ban service.
* `make clean`: Removes unused packages (`autoremove`) and clears the package cache (`clean`).
