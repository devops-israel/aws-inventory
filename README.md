# AWS Inventory

A single-file that shows the whole inventory of your AWS services on a single page.

## Usage

* Clone or copy the `index.html` file to your computer
* Open the `index.html` file in your browser

## How it looks

![screenshot](/example-screenshot.png?raw=true "Example AWS Inventory")

## How it works

The AWS Inventory is using the AWS JavaScript SDK and a sprinkle of Bootstrap,
this allows to show results in pretty tables from any AWS API.

The syntax to describe table headers and a pointer to the relevant array in the
results is using JMESPath syntax (jmespath.org).

Example of the EC2 listing:

    { service: "EC2",
      api: "describeInstances",
      title: "EC2 Instances",
      id: "ec2-instances",
      jmespath: "Reservations[].Instances",
      headings: ["InstanceId", "InstanceType", "ImageId", "LaunchTime", "KeyName", "State.Name"]
    }

This specifies that it should use the `AWS.EC2()` APIs, and call the
`describeInstances` method. Then create HTML elements that include the `id`
`ec2-instances` and a button with the title `EC2 Instances`.

The returned results, as documented in callback section for `describeInstances`
in the official documentation, are searched for `Reservations[].Instances` for
an array of relevant data to be put into a table.

https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeInstances-property

The table will include the headers described in `headings`, which also use
JMESPath, like in the example for `State.Name` so that nested elements can be
references.

## Notes

The AWS JavaScript SDK does not support all the AWS services when used in a
browser, because not all services have CORS enabled.

The list of CORS supported services is available at
https://github.com/aws/aws-sdk-js/blob/master/SERVICES.md

## Contributing

We follow the "fork-and-pull" Git workflow.

* Fork the repo on GitHub
* Clone the project to your own machine
* Commit changes to your own branch
* Push your work back up to your fork
* Submit a Pull request so that we can review your changes and merge

## Copyright and Licensing

MIT License, as described in the `LICENSE` file

Copyright 2018 &copy; Devops Israel, Evgeny Zislis and contributors
