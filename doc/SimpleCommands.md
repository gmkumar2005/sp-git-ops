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
oc delete PipelineRun sp-lr-pipeline-run-1  -n odh-dev && oc apply -f pipelinerun.yaml -n odh-dev  &&tkn pipelinerun logs sp-lr-pipeline-run-1 -f -n odh-dev

```

## Run the container
```

oc run sp-lr-classifier-image -ti --image=image-registry.openshift-image-registry.svc:5000/odh-dev/sp-lr-classifier-image:latest --rm=true --restart=Never -- bash

```

## Environment variables
```
  # s3_endpoint_url = 'http://13.67.138.157:8000'
    # s3_access_key = 'opendatahub'
    # s3_secret_key = 'b3BlbmRhdGFodWI='
    # #s3_bucket = os.environ['BUCKET']
    # s3_bucket="frauddetection"


    export S3_ENDPOINT_URL="http://13.67.138.157:8000"
    export S3_ACCESS_KEY="opendatahub"
    export S3_SECRET_KEY="b3BlbmRhdGFodWI="
    export S3_BUCKET="frauddetection"
    export MAX_KEYS=40

s3_endpoint_url="http://13.67.138.157:8000"
s3_access_key="opendatahub"
s3_secret_key="b3BlbmRhdGFodWI="
s3_bucket="frauddetection"
max_keys=40


=

    click.echo('s3_endpoint_url: %s' % s3_endpoint_url)
    click.echo('s3_access_key: %s' % s3_access_key)
    click.echo('s3_secret_key: %s' % s3_secret_key)
    click.echo('s3_bucket: %s' % s3_bucket)


```