Loops are used to iterate over a set of values, such as a simple list of strings, or a list of dictionaries.

Conditionals are used to execute tasks or plays only when certain conditions have been met.

Handlers are special tasks that execute at the end of the play if notified by other tasks.

Handlers are only notified when a task reports that it changed something on a managed host.

Tasks can be configured to handle error conditions by ignoring task failure, forcing handlers to be called even if the task failed, marking a task as failed when it succeeded, or overriding the behavior that causes a task to be marked as changed.

Blocks are used to group tasks as a unit and to execute other tasks depending upon whether all the tasks in the block succeed.
