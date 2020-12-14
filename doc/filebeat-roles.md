# Filebeat roles

## filebeat_monitoring

### Cluster
`monitoring`

### Indices
`create_index` on `.monitoring-beats-*`

`create_doc` on `.monitoring-beats-*`

![](.filebeat-user_images/3f828596.png)


## filebeat_pipelines

### Cluster
`manage_ingest_pipelines` `manage_index_templates`

![](.filebeat-user_images/60869969.png)

## filebeat_setup

### Cluster
`monitor` `manage_ilm` `manage_ml`

### Indices
`manage` `write` `read` on `filebeat-*`

![](.filebeat-user_images/37b83ef2.png)
