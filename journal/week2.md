# Week 2 — Distributed Tracing

## Pillars of Observability
Observability is about instrumenting systems to gather useful data that tells you when and why systems are behaving in a certain way. Whenever a system develops a fault, you should first examine telemetry data to better understand why the error occurred.

- Logs
- Metrics
- Tracing

### Logs
Logs are structured and unstructured lines of text a system produces when certain codes run. In general, you can think of a log as a record of an event that happened within an application. Logs help uncover unpredictable and emergent behaviors exhibited by components of microservices architecture.

### Metrics
Metrics are a numerical representation of data that can be used to determine a service or component’s overall behavior over time. Metrics are a measured value derived from system performance. With Metrics, you can easily correlate them across infrastructure components to get a holistic view of system health and performance. They also enable easier querying and longer retention of data. You can gather metrics on system uptime, response time, the number of requests per second, and how much processing power or memory an application is using, for example. Typically, SREs and ops engineers use metrics to trigger alerts whenever a system value goes above a specified threshold. 

## Observability vs Monitoring
Monitoring is tooling or a technical solution that allows teams to watch and understand the state of their systems. Monitoring is based on gathering predefined sets of metrics or logs.

### Observability is tooling or a technical solution that allows teams to actively debug their system. Observability is based on exploring properties and patterns not defined in advance.

### Obeservability services in AWS

- AWS Cloudwatch logs
- AWS Cloudwatch metrics
- AWS X Ray traces

![image](https://user-images.githubusercontent.com/70094537/224244991-26ce039c-c668-4946-af56-b368a600874a.png)


Instrumentation is what helps you to create or produce logs metrics traces.



Log into honeycomb.io,create a new enviroment, copy your API key and create the gitpod env var
```sh
export HONEYCOMB_API_KEY=""
export HONEYCOMB_SERVICE_NAME="Cruddur"
gp env HONEYCOMB_API_KEY=""
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
```

Add the following Env Vars to `backend-flask` in docker compose -we are configuring OTEL (Open Telemetry) to send to Honeycomb

```yml
OTEL_SERVICE_NAME: 'backend-flask'
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "${HONEYCOMB_SERVICE_NAME}"
```

Add the following files to our `requirements.txt` - these packages help to instrument a Flask app with OpenTelemetry:
```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

Install these dependencies:

```sh
pip install -r requirements.txt
```

Add to the `app.py`

```py
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```


```py
# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)
```

```py
# Initialize automatic instrumentation with Flask
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

Added these ports to our gitpod.yml file
```
ports:
  - name: frontend
    port: 3000
    onOpen: open-browser
    visibility: public
  - name: backend
    port: 4567
    visibility: public
  - name: xray-daemon
    port: 2000
    visibility: public
```

## Tag homework

git tag week-(number)
git push --tags


To create span and attribute, add the following code on the home_activities.py
```
from opentelemetry import trace
tracer = trace.get_tracer("home.activities")
```

```
with tracer.start_as_current_span("home-activities-mock-data"):
    span = trace.get_current_span()
```
```
span.set_attribute("app.now", now.isoformat())
 ```
 at the end of the code, put the following
 ```
span.set_attribute("app.result_lenght", len(results))

 ```
 
  include this as a step in your gidpod.yml file so you dont have to run npm i all the time, it happens automatically.

 ```
 tasks:
  - name: react-js
    command: |
      cd frontend-react-js
      npm i
 ```


### AWS X-ray
add to app.py file
```py
# X-RAY ----------
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.ext.flask.middleware import XRayMiddleware


# X-RAY ----------
xray_url = os.getenv("AWS_XRAY_URL")
xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)

```
