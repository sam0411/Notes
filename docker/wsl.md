# WSL

## [MicroSoft Document](https://docs.microsoft.com/zh-cn/windows/wsl/setup/environment)

## WSL Command

```Shell
	# List available distribution 
	wsl --list --online

	# Install
	wsl --install
	wsl --install --distribution <Distribution Name>

	# List distribution already installed in Local
	wsl --list --verbose

	# Set default WSL version
	wsl --set-default-version <Version>
	wsl --set-version <distribution name> <versionNumber>
	wsl --set-default <Distribution Name>

	# WSL operations
	wsl --status
	wsl --shutdown
```