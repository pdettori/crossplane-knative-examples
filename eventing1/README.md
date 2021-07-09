Knative Eventing With Crossplane - Example 1

The code in this example is part of the Medium Blog `Build event-driven applications with Knative and Crossplane`.
Please reference the blog for details on how to use it.

Create Kafka Topic

`kubectl apply -f eventing1/topic-ref.yaml`

To check on the status of the topic use these commands: 

`kubectl describe topic fruits`
`kubectl get topic fruits`

To delete topic: 

`kubectl delete topic fruits`
