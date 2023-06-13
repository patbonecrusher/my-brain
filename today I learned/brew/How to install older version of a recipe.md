---
creation date: 2023-06-13 10:33
modification date: Tuesday, 13th June 2023, 10:33:12
tags: today_i_leaned, computer/macOS
---

# How to install older version of a recipe

1. Uninstall cmake `brew uninstall cmake`
2. Download the older version formula `curl -O https://raw.githubusercontent.com/Homebrew/homebrew-core/edfe4515af314e385143f917e503fa247ae67b6a/Formula/cmake.rb`
3. Install `brew install -s ./cmake.rb`
