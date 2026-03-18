# Makefile for Popular Programming Languages (Debian/Ubuntu)

.PHONY: help install-all update install-c install-python install-node install-rust install-go install-java

# Default target
help:
	@echo "Polyglot Developer Environment Installer"
	@echo "Usage:"
	@echo "  make install-all      - Installs C/C++, Python, Node.js, Rust, Go, and Java"
	@echo "  make install-[lang]   - Installs a specific language (e.g., make install-rust)"

install-all: update install-c install-python install-node install-rust install-go install-java
	@echo "================================================================"
	@echo "Installation complete! Note: You may need to restart your terminal"
	@echo "or source your profile (e.g., source ~/.bashrc) for Rust/Node paths to load."
	@echo "================================================================"

update:
	@echo "=> Updating system package repositories..."
	sudo apt-get update

install-c:
	@echo "=> Installing C/C++ (GCC/Make)..."
	sudo apt-get install -y build-essential

install-python:
	@echo "=> Installing Python 3 and pip..."
	sudo apt-get install -y python3 python3-pip python3-venv

install-node:
	@echo "=> Installing latest Node.js LTS via NodeSource..."
	# Downloads the official NodeSource setup script and installs Node/NPM
	curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
	sudo apt-get install -y nodejs

install-rust:
	@echo "=> Installing Rust via official Rustup script..."
	# Downloads and runs the official rustup installer non-interactively
	curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

install-go:
	@echo "=> Installing Go..."
	sudo apt-get install -y golang-go

install-java:
	@echo "=> Installing Java (Default OpenJDK)..."
	sudo apt-get install -y default-jdk
