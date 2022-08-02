========
Job Task
========

Tasks need to be set up only for non-numeric blocks where each task can have its own name and command.
For numeric blocks, tasks get generated automatically on demand and a numeric block has enough information to generate its tasks.
Most blocks are numeric, as tasks differ only by a few values (like frame numbers) in a command.

There are some cases where task commands differ in several strings and thus the block cannot describe them by frame numbers.
For example *ffmpeg* converts various sequences and movies in a single job block (Rules constructs such jobs for previews).

Python example on how to create a job with a non-numeric block and custom tasks:
.. code-block:: python

   import af

   job = af.Job(job_name)

   block = af.Block(name, service)

   job.blocks.append(block)

   task = af.Task(task_name)

   block.tasks.append(task)



Attributes
==========

If a block is set to be numeric, all this attributes are generated on the fly by the block.

name
----
``af.Task(str)``

Task name. Generated, if the block is numeric.

command
-------
``af.Task.setCommand(str)``

Command to execute. Generated, if the block is numeric.

files[]
-------
``af.Task.setFiles(str[])``

Files for preview. Generated, if the block is numeric.

environment
-----------
``af.Task.setEnv(name, value)``

Extra environment variables for the tasks process.
These variables will be merged with the blocks extra environment variables.

tst
---
Time when the task was started (last start).

tdn
---
Time when the task was done (last finish).

str
---
Number of times the task has been started (it can be manually or automatically restarted).

per
---
Progress percentage of the running task.

frm
---
Running frame for multiframe tasks.
Multiframe tasks can be produced by numeric blocks when the parameter "frames per render" is > 1.

pfr
---
Running percentage of current running frame for multiframe tasks which can be produced by numeric blocks when frames per render parameter > 1.

err
---

Number of times the task produced an error.

hst
---
Host name where the task was started last time.

act
---
Last task activity.
This is a sting to informate user only, does not influence anything.
Activity can be parsed from task process output by Python parser class.

State
=====

==================== ======= ===
Read                 ``RDY`` Task can be executed. 
Running              ``RUN`` Task is running. 
Done                 ``DON`` Task is done. 
Error                ``ERR`` Task finished with error or failed to start. 
Skipped              ``SKP`` Task skipped. 
Waiting Dependencies ``WD``  Warning dependent tasks to be done.
Warning              ``WRN`` Warning from parser. 
Parser Error         ``PER`` Error from parser. 
Parser Bad Result    ``PBR`` Bad result from parser. 
Restated Error Ready ``RER`` Automatically restarted ``ERR`` task.
==================== ======= ===

