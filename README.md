# Notes on implementing open-telemetry instrumentation in Python

## What is open-telemetry
open-telemetry is a open-source framnework for instrumenting software applications and systems. It's build on the earlier open-tracing and open-census projects.


# Unstructured Notes
## Random Links
* https://opentelemetry.io/docs/instrumentation/python/
* https://opentelemetry.io/docs/concepts/
* https://opentelemetry-python.readthedocs.io/ Core Python instrumentation library
* https://opentelemetry-python-contrib.readthedocs.io/ Python instrumentation for 3rd party libraries
* https://aws.amazon.com/blogs/opensource/auto-instrumenting-a-python-application-with-an-aws-distro-for-opentelemetry-lambda-layer/
* https://www.aspecto.io/blog/opentelemetry-collector-processors/


## Lessons Learned

Collector
* Used as an intermediary to collect otel data instead of sending it direct to your APM's server
* Rationale
  - You can run a copy of it alongside your application, so that connections are network-local (and hence more reliable and faster). This improves the behaviour of the instrumented application
  - You can add a processing pipeline to it, if you want to pre-process your data before sending it to your APM
  - You can run a copy inside your VPC if you have network restrictions on outbound traffic

"Auto" instrumentation. otel doco often refers to manual instrumentation vs. automatic instrumentation. This can mean *three* things (not two)
1. Write new code that creates spans and events within your application codebase. Thsi is called manual instrumentation
2. Use plugins for libraries (eg. web server frameworks and databse clients) to create spans and propagate context. This might be called manual instrumentation or auto-instrumentation, or might be contrasted with either or both of the above. 🤷
3. A magic wrapper for your application that auto-detects your libraries and instruments them (ie. a scan-and-patch variation of (2) above). This is called auto-instrumentation

## WHat's an APM I can use
* https://honeycomb.io
* SignalFX (now part of Splunk)
* https://lightstep.com/
* https://www.aspecto.io/
