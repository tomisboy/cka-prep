## We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.
`k drain node01  --ignore-daemonsets`

## The maintenance tasks have been completed. Configure the node node01 to be schedulable again.
`kubectl uncordon node01`

## Mark node01 as unschedulable so that no new pods are scheduled on this node.
`kubectl cordon node01`