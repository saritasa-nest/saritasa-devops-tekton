# Install
If you want to build and apply the changes

```bash
kustomize build apps/backend/pipelines | k apply -f -
```

# Run manually

You test your pipelines by creating ad-hoc pipeline runs, for example check out build-pipeline-run.yaml.
Increment the name for the run, i.e.

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: build-pipeline-run-1
```
to

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: build-pipeline-run-2
```

and then do:

```
k apply -f apps/backend/pipelines/build-pipeline-run.yml && time tkn pipelinerun logs build-pipeline-run-2 -f
```

or alternative (if you don't want to hassle by changing YAML manifest)

```bash
k delete pipelinerun build-pipeline-run-1
k apply -f apps/backend/pipelines/build-pipeline-run.yaml && time tkn pipelinerun logs build-pipeline-run-1 -f
```

# Run through similating the trigger event
See more details in tekton [README - how to test triggers](/cluster/tekton/README.md)
