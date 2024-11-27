# .spec.completions

Defaults to 1. Number of completions needed.

# .spec.parallelism

Defaults to 1.



# Non-parallel Jobs

Job that runs only one Pod unless the Pod fails. When the pod completes successfully, the Job is considered complete.
There’s no parallelism involved.

# Parallel Jobs with a fixed number of completions

These are tasks that start and run several Pods in parallel. The Job continues running until a specified number of
successful Pod .spec.completionscompletions have occurred. When using .spec.completionMode="Indexed", each Pod gets a
different index in the range 0 to .spec.completions-1. Another option is to set the spec.parallelism field to define the
number of parallel Jobs.

# Parallel Jobs with a Work Queue

running multiple tasks in parallel. They’re used when the process consists of several tasks, but none are dependent on
each other. The Pods must coordinate amongst themselves or an external service to determine what each should work on.
For example, a Pod might fetch a batch of up to N items from the work queue. Once at least one Pod has terminated with
success and all Pods are terminated, then the Job is completed with success.

For a work queue Job, you must leave .spec.completions unset, and set **.spec.parallelism** to a non-negative integer.