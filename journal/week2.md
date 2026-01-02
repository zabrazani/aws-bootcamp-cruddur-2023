# Week 2 — Distributed Tracing

## HoneyComb  

 
Honeycomb is a modern **observability platform** that helps software engineers, DevOps teams, and site reliability engineers (SREs) understand, debug, and optimize complex distributed systems in real time.  

---

## 🐝 What Honeycomb Is
- **Company:** Honeycomb (also known as Hound Technology, Inc.), founded in 2016, headquartered in San Francisco.  
- **Product:** A SaaS observability and application performance management (APM) platform.  
- **Purpose:** Enables developers to investigate issues in microservices, cloud-native apps, and distributed architectures quickly.  

---

## 🔑 Key Features
- **Event-based observability:** Honeycomb stores telemetry as events, not just metrics, giving richer context.  
- **Query Builder & BubbleUp:** Interactive tools to explore anomalies and pinpoint root causes.  
- **Service Map:** Visualizes how services interact, helping debug dependencies.  
- **SLOs (Service Level Objectives):** Track reliability goals and alert when thresholds are breached.  
- **OpenTelemetry integration:** Works with open-source instrumentation standards.  
- **AI-powered insights:** Newer versions include AI-native debugging assistants that accelerate investigations.  

---

## ⚖️ Why Teams Use Honeycomb
| Aspect                  | Honeycomb Advantage                                                                 |
|--------------------------|-------------------------------------------------------------------------------------|
| **Speed**               | Lightning-fast queries across large datasets                                    |
| **Scalability**         | Handles terabytes of telemetry data without slowing down                        |
| **Flexibility**         | Works with logs, traces, metrics, and custom events                          |
| **Collaboration**       | Helps engineers debug together with shared queries and visualizations           |
| **Cost Model**          | Event-based pricing that encourages exploration without surprise bills          |

---

## 🚀 Use Cases
- Debugging **microservices** in production.  
- Monitoring **real-time user behavior** in apps.  
- Investigating **performance bottlenecks** across distributed systems.  
- Ensuring **reliability** with SLO tracking.  

---

## ⚠️ Considerations & Trade-offs
- **Learning curve:** Engineers need to adopt event-based thinking, which differs from traditional metrics dashboards.  
- **Cost scaling:** While pricing is transparent, very high event volumes can still add up.  
- **Specialization:** Honeycomb is focused on observability; it doesn’t replace full monitoring suites like Prometheus or Grafana but complements them.  

---

**Bottom Line:** Honeycomb is designed for teams running **complex, distributed, cloud-native systems** who need deep visibility and fast debugging. It’s particularly valuable for organizations practicing DevOps and SRE, where uptime and performance are critical.  

Sources:   

When creating a new dataset in HoneyComb it will provide all these installation intructions  

Steps that I followed  

1. Login to HoneyComb
2. Create an Environment named bootcamp

3. Grab the API keys from the honeycomb account anf run this command

```sh
export HONEYCOMB_API_KEY="KMpsdaCmeIMrszgfDvguMO"
env HONEYCOMB_API_KEY="KMpsdaCmeIMrszgfDvguMO"
env | grep HONEY
export HONEYCOMB_SERVICE_NAME="Cruddur"
env HONEYCOMB_SERVICE_NAME="Cruddur"
```

### Add teh following Env Vars to `backend-flask` in the docker compose  

4. Set up OTEL for backend in docker compose yml especially if you are running different 2 or more programs
`OTEL_SERVICE_NAME: "backend-flask"`
```
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=KMpsdaCmeIMrszgfDvguMO"
OTEL_SERVICE_NAME: "${HONEYCOMB-SERVICE_NAME}"

```

5. When Craeting a new Dataset in HoneyComb  it will pprovide all the installion instructions in the homepage
I am installing via phython.

```
cd backend-flask
python -m pip install opentelemetry-instrumentation

```
We will add ther remaining installations to this requirements to our backend-flask `requirements.txt`  

```
opentelemetry-instrumentation
opentelemetry-distro 
opentelemetry-exporter-otlp

```
 Next, install the instrumentation libraries for packages used in your application:
`opentelemetry-bootstrap --action=install`

6. Add to `app.py`

```py
# Honeycomb OpenTelemetry setup
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor

# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer . trace.get_tracer(_name_)

app = Flask(__name__)

# Honeycomb ------
# Initialize automatic instrumentation with Flask
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()

```
