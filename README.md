# [Amazon SNS](http://aws.amazon.com/sns/) Input for [Mozilla Heka](http://hekad.readthedocs.org/en/latest/)

A Mozilla Heka Input for Amazon Web Services SNS.

The Amazon SNS input will start a webserver on the given port and act as an endpoint for consuming topic messages per the [API instructions](http://docs.aws.amazon.com/sns/latest/dg/SendMessageToHttp.html).

Messages generated from the Amazon SNS Input will have a message type of `amazon.sns`.

# Installation

* You will need to setup delivery of an Amazon SNS topic to an HTTP/S endpoint.

* Create or add to the file {heka_root}/cmake/plugin_loader.cmake

```
add_external_plugin(git https://github.com/bellycard/heka-sns-input master)
```

* Build Heka per normal instructions for your platform.

Additional instructions can be found in the [Heka documentation for external plugins](http://hekad.readthedocs.org/en/latest/installing.html#build-include-externals).

# Parameters

- address (string, optional)
    The IP address and port for the HTTP/S webserver to listen for SNS POST
    actions.
    (default: 0.0.0.0:8225)
- verify_signatures (bool, optional)
    Whether or not the signature of the SNS message should be verified against
    Amazon's signature. This will incur processing overhead but will increase
    authenticity of messages delivered.
    (default: false)
- emit_in_payload (bool, optional)
    Specifies whether or not notification data should be written to outgoing
    message payloads, in JSON format as generated by Amazon SNS. If false
    notification data will be written to outgoing message fields.
    (default: true)

## Example Amazon SNS Input Configuration File

```
[Amazon RDS Notifications]
type = "AmazonSnsInput"
address = "0.0.0.0:8225"
emit_in_payload = true
verify_signatures = false
```
