# sam init<a name="sam-cli-command-reference-sam-init"></a>

Initializes a serverless application with an AWS SAM template\. The template provides a folder structure for your Lambda functions, and is connected to an event source such as APIs, S3 buckets, or DynamoDB tables\. This application includes everything you need to get started and to eventually extend it into a production\-scale application\.

**Usage:**

```
sam init [OPTIONS]
```

**Examples:**

```
Initializes a new SAM project using Python 3.6 default template runtime

$ sam init --runtime python3.6

Initializes a new SAM project using custom template in a Git/Mercurial repository

# gh being expanded to github url
$ sam init --location gh:aws-samples/cookiecutter-aws-sam-python

$ sam init --location git+ssh://git@github.com/aws-samples/cookiecutter-aws-sam-python.git

$ sam init --location hg+ssh://hg@bitbucket.org/repo/template-name

$ sam init --location hg+ssh://hg@bitbucket.org/repo/template-name

Initializes a new SAM project using custom template in a Zipfile

$ sam init --location /path/to/template.zip

$ sam init --location https://example.com/path/to/template.zip

Initializes a new SAM project using custom template in a local path

$ sam init --location /path/to/template/folder
```

**Options:**


****  

| Option | Description | 
| --- | --- | 
|  \-l, \-\-location TEXT | The template location \(Git, Mercurial, HTTP/HTTPS, ZIP, path\)\. | 
| \-r, \-\-runtime \[python3\.7\| python3\.6\| python2\.7\| python\| ruby2\.5\| nodejs6\.10\| nodejs8\.10\| nodejs\| dotnetcore2\.0\| dotnetcore2\.1\| dotnetcore1\.0\| dotnetcore\| dotnet\| go1\.x\| go\| java8\| java\] | The Lambda runtime of your application\. | 
| \-o, \-\-output\-dir PATH | The location where the initialized application is output\. | 
| \-n, \-\-name TEXT | The name of your project to be generated as a folder\. | 
| \-\-no\-input | Disables prompting and accepts default values that are defined in the template configuration\. | 
|  \-\-debug | Turns on debug logging\. | 
| \-h, \-\-help  | Shows this message and exits\. | 