# Gemini CLI Tools

A curated collection of essential CLI tools and guidelines for Gemini CLI to enhance productivity and automation.

## Overview

This project provides a comprehensive toolkit configuration for Gemini CLI, featuring:

- **Smart Tool Selection**: Prioritizes specialized CLI tools over generic approaches
- **Auto-Installation**: Automatically checks and installs missing tools
- **Cross-Platform Support**: Works on macOS, Linux, and Windows
- **Fallback Strategy**: Uses default Gemini behavior when no suitable tools are available

## How It Works

The system follows a 5-step process:

1. **Tool Review** - Checks all available tools for task suitability
2. **Installation Check** - Verifies if the selected tool is installed
3. **Auto-Install** - Installs missing tools automatically
4. **Execute** - Runs the task using the specialized tool
5. **Fallback** - Uses default Gemini methods if no tools match

## Included Tools

### Media & Downloads
- **yt-dlp** - Advanced video/audio downloader
- **ffmpeg** - Multimedia processing framework
- **wget** - File downloader with advanced features

### Web & APIs
- **curl** - HTTP client for API testing and web interactions

### Data Processing
- **jq** - JSON processor and transformer
- **ripgrep (rg)** - Ultra-fast text search
- **fd** - Modern file finder

### Development
- **git** - Version control system

### System & Files
- **rsync** - File synchronization tool
- **tree** - Directory structure visualizer
- **htop** - Interactive system monitor

## Usage

Simply use the `GEMINI.md` file as your prompt/configuration for Gemini CLI. The system will automatically:

- Identify the best tool for your task
- Check if it's installed
- Install it if needed
- Execute your request using the appropriate tool

## Benefits

- ⚡ **Faster execution** with specialized tools
- 🔧 **Automatic setup** - no manual installation needed
- 🎯 **Better results** - tools designed for specific tasks
- 🔄 **Reliable fallback** - always works even without tools
- 📚 **Comprehensive coverage** - handles most common CLI tasks

## Requirements

- Gemini CLI
- Internet connection (for tool installation)
- Package manager (Homebrew on macOS, apt on Ubuntu, Chocolatey on Windows)

---

*This toolkit is designed to make Gemini CLI more powerful and efficient by leveraging the best open-source CLI tools available.*
