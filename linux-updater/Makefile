# Makefile for Linux System Update and Security Hardening (Debian/Ubuntu)

.PHONY: help all update install-security configure-security clean

# Default target when just typing 'make'
help:
	@echo "Linux Security Automation Makefile"
	@echo "Usage:"
	@echo "  make all               - Run updates, install tools, and clean up"
	@echo "  make update            - Update package lists and upgrade system"
	@echo "  make install-security  - Install ufw, fail2ban, rkhunter, etc."
	@echo "  make clean             - Remove unused packages and clear cache"

all: update install-security configure-security clean
	@echo "System update and security installation complete."

update:
	@echo "=> Updating package lists and upgrading system..."
	sudo apt-get update
	sudo apt-get upgrade -y
	sudo apt-get dist-upgrade -y

install-security:
	@echo "=> Installing baseline security software..."
	# ufw: Uncomplicated Firewall
	# fail2ban: Prevents brute-force attacks
	# rkhunter: Rootkit scanner
	# unattended-upgrades: Automatic security updates
	# libpam-tmpdir: Secures temporary directory creation
	sudo apt-get install -y ufw fail2ban rkhunter unattended-upgrades libpam-tmpdir

configure-security:
	@echo "=> Configuring basic firewall rules..."
	# WARNING: If you are connected via SSH, ensure port 22 is allowed before enabling!
	sudo ufw allow ssh
	sudo ufw default deny incoming
	sudo ufw default allow outgoing
	sudo ufw --force enable
	@echo "=> Enabling Fail2Ban service..."
	sudo systemctl enable fail2ban
	sudo systemctl start fail2ban

clean:
	@echo "=> Cleaning up unused packages..."
	sudo apt-get autoremove -y
	sudo apt-get clean
