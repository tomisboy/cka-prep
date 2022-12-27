## We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment (env)?
`k get pods --selector env=dev`

## How many objects are in the prod environment including PODs, ReplicaSets and any other objects?
`kubectl get all --selector env=prod`

## Identify the POD which is part of the prod environment, the finance BU and of frontend tier?
` kubectl get all --selector env=prod,bu=finance,tier=frontend`
