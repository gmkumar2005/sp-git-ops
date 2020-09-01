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

### Execute the pipeline

```
@click.option('--s3_endpoint_url', envvar='S3_ENDPOINT_URL')
@click.option('--s3_access_key', envvar='S3_ACCESS_KEY')
@click.option('--s3_secret_key', envvar='S3_SECRET_KEY')
@click.option('--s3_bucket', envvar='S3_BUCKET')
@click.option('--max_keys', envvar='MAX_KEYS',type=int)

python /microservice/pipeline_step.py --s3_endpoint_url="http://13.67.138.157:8000" --s3_access_key="opendatahub"  --s3_secret_key="b3BlbmRhdGFodWI=" --s3_bucket="frauddetection" --max_keys="45"

python /microservice/test.py --s3_endpoint_url="http://13.67.138.157:8000" --s3_access_key="opendatahub"  --s3_secret_key="b3BlbmRhdGFodWI=" --s3_bucket="frauddetection" --max_keys="45"

```

## Run Executionpipeline
```
oc delete PipelineRun lr-experiment-1  -n odh-dev && oc apply -f pipelinerun.yaml -n odh-dev  &&tkn pipelinerun logs lr-experiment-1 -f -n odh-dev

```

## Creating values for secters
```
echo "s3_endpoint_url : " && echo -n 'http://13.67.138.157:8000' | base64
echo "s3_access_key : " && echo -n 'opendatahub' | base64
echo "s3_secret_key : " && echo -n 'b3BlbmRhdGFodWI=' | base64
echo "s3_bucket : " &&  echo -n 'frauddetection' | base64

```

### Run sp-classifier-pipeline
```
cd sp-classifier
oc delete PipelineRun sp-classifier-pipeline-run-1  -n odh-dev && oc apply -f pipelinerun.yaml -n odh-dev  &&tkn pipelinerun logs sp-classifier-pipeline-run-1 -f -n odh-dev

```

### Execute rf image
```
oc run sp-rf-classifier-image -ti --image=image-registry.openshift-image-registry.svc:5000/odh-dev/sp-rf-classifier-image:latest --rm=true --restart=Never -- bash

python /microservice/pipeline_step.py --s3_endpoint_url="http://13.67.138.157:8000" --s3_access_key="opendatahub"  --s3_secret_key="b3BlbmRhdGFodWI=" --s3_bucket="frauddetection" --max_keys="45"

```

### execute experiment pipeline
```

oc delete PipelineRun sp-experiment-1  -n odh-dev && oc apply -f pipelinerun.yaml -n odh-dev  &&tkn pipelinerun logs sp-experiment-1 -f -n odh-dev

```