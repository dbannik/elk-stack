# monolog pipelines

## Create a new pipeline
![](.monolog-pipeline_images/c8cbb51c.png)

## Add a `Grok` processor
![](.monolog-pipeline_images/d958e3a6.png)

#### Field `message`
#### Patterns 
```text
\[%{TIMESTAMP_ISO8601:timestamp}\] %{DATA:logger}.%{LOGLEVEL:level}: %{GREEDYDATA:message}
```
#### Ignore failure `true`
