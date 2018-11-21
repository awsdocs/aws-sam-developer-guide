# Install the AWS SAM CLI Using Pip<a name="serverless-sam-cli-install-using-pip"></a>

Install the AWS SAM CLI using pip by following these steps:

1. Verify that the Python version is 2\.7 or 3\.6\.

   ```
   $ python --version
   ```

   If it isn't installed, [download and install Python](https://www.python.org/downloads/)\.

1. Verify that pip is installed\.

   ```
   $ pip --version
   ```

   If it isn't installed, [download and install pip](https://pip.pypa.io/en/stable/installing/)\.

1. Install `aws-sam-cli`\.

   ```
   pip install --user aws-sam-cli
   ```

1. Adjust your `PATH` to include the Python scripts that are installed under the user's home directory\.
   + **Linux:** [Adjusting Path on Linux](serverless-sam-cli-install-linux-path.md)\.
   + **Windows:** [Adjusting Path on Windows](serverless-sam-cli-install-windows-path.md)\.
   + **macOS:** [Adjusting Path on macOS](serverless-sam-cli-install-mac-path.md)\.

1. Verify that `sam` is installed\.

   Restart or open a new terminal, and verify that the installation worked\.

   ```
   # Restart current shell
   $ sam --version
   ```