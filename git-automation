# Makefile for Automating Git Revisions and Releases

.PHONY: help init status commit patch minor major push

# Default commit message if none is provided: make commit MSG="your message"
MSG ?= "chore: auto-commit updates"

# Reads the current version from the VERSION file. 
CURRENT_VERSION = $(shell cat VERSION 2>/dev/null || echo "0.0.0")

help:
	@echo "Git Revision Automation"
	@echo "-----------------------"
	@echo "Usage:"
	@echo "  make init      - Initialize the VERSION file (starts at 0.0.0)"
	@echo "  make status    - Show current git status"
	@echo "  make commit MSG=\"msg\" - Add all changes and commit"
	@echo "  make patch     - Bump patch version (x.y.Z+1), tag, and commit"
	@echo "  make minor     - Bump minor version (x.Y+1.0), tag, and commit"
	@echo "  make major     - Bump major version (X+1.0.0), tag, and commit"
	@echo "  make push      - Push commits and tags to the remote repository"

init:
	@if [ ! -f VERSION ]; then echo "0.0.0" > VERSION; echo "=> VERSION file created at 0.0.0"; else echo "=> VERSION file already exists."; fi

status:
	git status

commit:
	@echo "=> Staging all changes and committing..."
	git add .
	git commit -m "$(MSG)"

# Version bumping using awk to iterate the semantic numbers
patch:
	@echo $(CURRENT_VERSION) | awk -F. '{printf "%d.%d.%d", $$1, $$2, $$3+1}' > VERSION
	@$(MAKE) _tag_release TYPE="Patch"

minor:
	@echo $(CURRENT_VERSION) | awk -F. '{printf "%d.%d.0", $$1, $$2+1}' > VERSION
	@$(MAKE) _tag_release TYPE="Minor"

major:
	@echo $(CURRENT_VERSION) | awk -F. '{printf "%d.0.0", $$1+1}' > VERSION
	@$(MAKE) _tag_release TYPE="Major"

# Internal helper target for staging the VERSION file and creating the git tag
_tag_release:
	@echo "=> Creating $(TYPE) release..."
	git add VERSION
	git commit -m "chore: bump version to v$(shell cat VERSION)"
	git tag -a "v$(shell cat VERSION)" -m "Release v$(shell cat VERSION)"
	@echo "=> Version successfully bumped to v$(shell cat VERSION)"

push:
	@echo "=> Pushing commits and tags to remote..."
	git push origin HEAD
	git push origin --tags
