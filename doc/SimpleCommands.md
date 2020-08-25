## Project list
```
hl7-labs-kamel
hl7-nurse-charting
hl7-vitals
hl7-medication
hl7-microlab
hl7-patient
sp-ft-transformer
sp-hlf-classifier
sp-lr-classifier
sp-dt-classifier
sp-gb-classifer
sp-rf-classifier
sp-xg-classifier
sp-seldon-model
sp-seldon-explanation
sp-git-ops
```

## Pipeline run commands
```
oc delete PipelineRun nlp-pipeline-run-1  -n odh-dev && oc apply -f pipelinerun.yaml -n odh-dev  &&tkn pipelinerun logs nlp-pipeline-run-1 -f -n odh-dev

```