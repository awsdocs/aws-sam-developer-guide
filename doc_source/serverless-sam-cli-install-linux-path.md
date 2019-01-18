# Adjusting Your Path on Linux<a name="serverless-sam-cli-install-linux-path"></a>

This section describes how you can adjust your path\. You have to do this as part of installing the AWS SAM CLI by using pip, as described in [Installing Using Pip](serverless-sam-cli-install-additional.md#serverless-sam-cli-install-using-pip)\.

On Linux systems, the command `python -m site --user-base` typically prints `~/.local` path, so you need to add `/bin` to obtain the script path\.

**Note**  
As explained in the [Python Developer's Guide](https://www.python.org/dev/peps/pep-0370/#specification), the user's home directory \(where the scripts are installed\) is `~/.local/bin` for Linux\.

```
# Find your Python User Base path (where Python --user will install packages/scripts)
$ USER_BASE_PATH=$(python -m site --user-base)

# Update your preferred shell configuration
-- Standard bash --> ~/.bash_profile
-- ZSH           --> ~/.zshrc
$ export PATH=$PATH:$USER_BASE_PATH/bin
```

Restart or open a new terminal, and verify that the installation worked:

```
# Restart current shell
$ exec "$SHELL"
$ sam --version
```